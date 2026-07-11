<a href="../README.md">Back to README</a>

# .profile vs .bashrc on WSL2

## Why WSL is different from a normal Linux terminal

On most Linux desktop terminals, opening a new tab starts a non-login interactive shell, so `.bashrc` is read and `.profile` is usually not part of that startup path.

On WSL2, Bash is commonly launched by `wsl.exe` as a login + interactive shell, so `.profile` runs and then sources `.bashrc` as part of the same startup sequence each time a new terminal window or tab is opened.

## The convention, and the choice made here

The standard split is:

- Login-scope environment and PATH exports in `.profile`
- Interactive-only setup in `.bashrc` (prompt, aliases, completions, interactive helpers)

Two valid approaches exist:

1. Keep most setup centralized in `.bashrc`
2. Keep guarded PATH/env exports in `.profile`, keep interactive setup in `.bashrc`

This repo uses option 2. It aligns with login-scope conventions and also protects against a bare non-login `bash` started from within an already-running shell.

## Ordering is a hard requirement

Because `.bashrc` is sourced from `.profile`, any tool initialized in `.bashrc` via `eval` (for example Oh My Posh and uv/uvx completions) must already be discoverable on `PATH`.

That means the `.profile` block that sources `.bashrc` must stay last, after all PATH/env exports.

## Canonical structure

Use this exact order in `.profile`:

1. umask comment (unchanged)
2. Guarded PATH block for `$HOME/bin`
3. Guarded PATH block for `$HOME/.local/bin`
4. Plain env/PATH exports (`UV_NO_MODIFY_PATH`)
5. LAST: the `if running bash ... source ~/.bashrc` block

`.bashrc` keeps interactive-only setup: prompt initialization, uv/uvx completion evals, nvm loading, aliases.

## Adding new exports safely

For any future install step that needs to add PATH/env exports to `.profile`, use this anchor-based, idempotent insertion pattern. Do not use blind `>>` append for `.profile` exports in this repo.

```bash
PROFILE="$HOME/.profile"
ANCHOR='^# if running bash$'
MARKER='<unique string from this block, e.g. env var name>'

if ! grep -q "$MARKER" "$PROFILE"; then
    if grep -q "$ANCHOR" "$PROFILE"; then
        sed -i "/$ANCHOR/i\\
# <comment>\\
export VAR=value\\
" "$PROFILE"
    else
        echo "WARNING: anchor line not found in $PROFILE - appending to end instead, check ordering manually" >&2
        printf '\n# <comment>\nexport VAR=value\n' >> "$PROFILE"
    fi
fi
```

Why this is required:

- Blind append can break required ordering by placing exports after the `.bashrc` source block.
- The anchor existence check prevents a silent no-op if the anchor line is missing or changed.

## How to verify

After any change, open a genuinely new WSL terminal (new login shell) and run:

- `echo "$PATH" | tr ':' '\n' | sort | uniq -d` -> expected: no output (no duplicates)
- `echo "$PATH" | tr ':' '\n' | grep -E "\.local/bin"` -> expected: present once
- `complete -p uv uvx` -> expected: shows registered `_uv`/`_uvx` completion functions, no errors
- `oh-my-posh --version` -> expected: prints a version, no shell-start error

Do not rely only on `source ~/.profile` for this validation.

<a href="../README.md">Back to README</a>
