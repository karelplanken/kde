# WSL 2 Ubuntu Shell Initialization

This guide explains how shell initialization works in WSL 2 Ubuntu and how to properly manage the $PATH environment variable to avoid duplication and ensure user-installed binaries are accessible.

When opening a WSL 2 Ubuntu terminal from within Windows Terminal or from start, `.profile` is sourced first. In `.profile`, `.bashrc` is sourced and after `.bashrc` finishes, control returns to `.profile`. `.profile` then continues executing the remaining lines. This means that for this setup `.bashrc` is not sourced independently when launching Ubuntu from Windows Terminal, it's sourced only because `.profile` tells it to. Therefore, `.profile` is the true entry point for the shell session in this context. I noticed this because adding `~/.local/bin` in `.bashrc` resulted in a duplicate entry in `$PATH`. Now `.bashrc` is sourced in `.profile` before the `~/.local/bin` logic adds `~/.local/bin` to `$PATH`. However, `~/.local/bin` must be added in `.bashrc` before invoking applications that are installed in `~/.local/bin`. So I think the best practice for this case is, since `.profile` is always sourced first and it sources `.bashrc`, the cleanest and most robust setup is to conditionally add `~/.local/bin` to `$PATH` in `.profile`. In `.profile` I keep this block:

```bash
if [ -n "$BASH_VERSION" ]; then
    if [ -f "$HOME/.bashrc" ]; then
        . "$HOME/.bashrc"
    fi
fi
```

and I change:

```bash
# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/.local/bin" ]; then
    PATH="$HOME/.local/bin:$PATH"
fi
```

to:

```bash
# set PATH so it includes user's private bin if it exists and if it's not already in $PATH
if [[ -d "$HOME/.local/bin" && ! ":$PATH:" == *":$HOME/.local/bin:"* ]]; then
    PATH="$HOME/.local/bin:$PATH"
fi
```

Since `~/.local/bin` is added to `$PATH` conditionally in `.bashrc`:

```bash
# Set $PATH so it includes user's private bin if it exists
if [ -d "$HOME/.local/bin" ] && [[ ":$PATH:" != *":$HOME/.local/bin:"* ]]; then
  export PATH="$HOME/.local/bin:$PATH"
fi
```

I make sure that `~/.local/bin` always is in `$PATH` and no duplicates are introduced. To check if `~/.local/bin` is in `$PATH` and that there's only a single instance of it in `$PATH`, run:

```bash
echo $PATH | grep "$HOME/.local/bin"
```

