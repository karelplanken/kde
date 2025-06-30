<a href="../README.md">Back to README</a>

# uv on Ubuntu

This document describes how to install and configure uv, a fast Python package manager, on Ubuntu with Bash running in Windows Terminal. The Ubuntu is installed in WSL2 on Windows 11. If you're using a different shell (e.g., Zsh), refer to the uv documentation for shell-specific instructions. These instructions follow the official [uv documentation](https://docs.astral.sh/uv/) for installing uv on Linux and include steps for verification, updating, and enabling shell autocompletion.

# Installing uv on Ubuntu

Install uv on Ubuntu (in WSL2) using the standalone installer:

```bash
# On macOS and Linux.
curl -LsSf https://astral.sh/uv/install.sh | sh
```

After uv, you can check that uv is available by running the `uv` command:

```bash
uv
```

You should see output similar to: An extremely fast Python package manager.

## Enable Shell Autocompletion

To enable shell autocompletion for uv commands, run the following:

```bash
echo "\n# Shell completion for uv" >> ~/.bashrc
echo 'eval "$(uv generate-shell-completion bash)"' >> ~/.bashrc
```

To enable shell autocompletion for uvx commands, execute:

```bash
echo "\n# Shell completion for uvx" >> ~/.bashrc
echo 'eval "$(uvx --generate-shell-completion bash)"' >> ~/.bashrc
```

For changes to take effect, restart the current shell to apply changes:

```bash
exec $_SHELL
```

## Updating uv

When uv is installed via the standalone installer, it can update itself on-demand:

```bash
uv self update
```

<a href="../README.md">Back to README</a>