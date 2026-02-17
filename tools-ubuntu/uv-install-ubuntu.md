<a href="../README.md">Back to README</a>

# uv on Ubuntu

This document describes how to install and configure uv, a fast Python package manager, on Ubuntu with Bash running in Windows Terminal. The Ubuntu is installed in WSL 2 on Windows 11. If you're using a different shell (e.g., Zsh), refer to the uv documentation for shell-specific instructions. These instructions follow the official [uv documentation](https://docs.astral.sh/uv/) for installing uv on Linux and include steps for verification, updating, and enabling shell autocompletion.

## Why uv?

Previously I used pyenv with the pyenv-virtualenv plugin after I was sort of done with pip. Pyenv did a great job managing various Python versions and virtual environments. Now uv has caught my attention and I think this is a fantastic tool. [uv](https://docs.astral.sh/uv/) is a drop-in replacement for pip, pip-tools, pipx, poetry, pyenv, twine, virtualenv, and more.

But why do we need these tools? Operating systems often rely on a specific version of Python, so modifying the system Python can break critical functionality. As developers, we should avoid altering the system Python. Moreover, working on Python projects may introduce dependencies on specific packages or modules (libraries) or even a dependency in the form of a specific Python version. To address these challenges, we should manage our own Python versions and avoid installing Python or packages globally. Furthermore, we should work in virtual environments to restrict the packages to the specific project. All these requirements are quite easily met when working with a great tool like uv.

## Installing uv on Ubuntu

Install uv on Ubuntu (in WSL 2) using the standalone installer:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

After installing uv, you can check that uv is available by running the `uv` command:

```bash
uv
```

You should see output similar to: An extremely fast Python package manager.

Since `~/.local/bin` is already manually added to `$PATH`, which is where uv installs itself, we don't want uv 
to also add `~/.local/bin` and create a duplicate entry. Therefore add following lines to `.bashrc` by running:

```bash
echo "\n# Prevent uv from modifying shell profiles during updates" >> ~/.bashrc
echo "export UV_NO_MODIFY_PATH=1" >> ~/.bashrc
```


## Enable Shell Autocompletion

1. To enable shell autocompletion for uv commands, run the following:

    ```bash
    echo -e "\n# Shell completion for uv" >> ~/.bashrc
    echo 'eval "$(uv generate-shell-completion bash)"' >> ~/.bashrc
    ```

2. To enable shell autocompletion for uvx commands, execute:

    ```bash
    echo -e "\n# Shell completion for uvx" >> ~/.bashrc
    echo 'eval "$(uvx --generate-shell-completion bash)"' >> ~/.bashrc
    ```

    Note: uvx is a companion tool to uv that allows you to run Python scripts in ephemeral, isolated environments without needing to manually create virtual environments.

3. For changes to take effect, restart the current shell to apply changes:

    ```bash
    source ~/.bashrc
    ```

4. Verify the install by running:

    ```bash
    uv
    ```

    You should see output starting with: "An extremely fast Python package manager."

5. Verify the uv version:

    ```bash
    uv --version
    ```

## Updating uv

To check if a new uv version is available, compare the output of:

```bash
curl -s https://api.github.com/repos/astral-sh/uv/releases/latest | grep tag_name
```

with the current uv version.

When uv is installed via the standalone installer, it can update itself on-demand:

```bash
uv self update
```

<a href="../README.md">Back to README</a>