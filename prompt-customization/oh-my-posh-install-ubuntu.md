<a href="../README.md">Back to README</a>

# Oh My Posh on Ubuntu

To enhance the terminal experience and improve readability, I customize the Bash prompt using [Oh My Posh](https://ohmyposh.dev/). This will also benefit working with Git. Of course you can find all instructions in the official docs.

## General Notes and Considerations

This short guide is part of my dev setup for Windows with WSL 2 and assumes you have already installed PowerShell, Windows Terminal, and WSL 2 with Ubuntu. On my system, Ubuntu is accessed through either the Windows Terminal or the integrated terminal in VS Code. Therefore the installation of Oh My Posh in WSL Ubuntu doesn't require a specific Nerd font to be available within Ubuntu.

For details on shell initialization and details on `.profile` and `.bashrc` in WSL 2, see <a href="../additional-info/wsl2-shell-initialization.md">WSL 2 Ubuntu Shell Initialization</a>.

## Verify/Install Unzip

To install Oh My Posh, we need Unzip, so make sure it is installed by checking its version:
  
```bash
unzip -V
```

if you get a `command not found` error, then install unzip:

```bash
sudo apt install unzip
```

## Install Oh My Posh

Note: Except for AArch64/ARM64, Oh My Posh can be installed using Homebrew. However, Oh My Posh installed with Homebrew may cause issues after upgrading, such as the terminal becoming temporarily unresponsive and displaying errors about missing previous versions. To avoid these issues, I recommend installing Oh My Posh manually using the shell script.

1. Install Oh My Posh:

    ```bash
    curl -s https://ohmyposh.dev/install.sh | bash -s
    ```
    
2. I assume here that `oh-my-posh` ended up in `~/.local/bin`. You can check this by running:

    ```bash
    [ -f "$HOME/.local/bin/oh-my-posh" ] && echo "True" || echo "False"
    ```

    If you get True then all is well and you can proceed. If you get False then Oh My Posh, i.e. the executable oh-my-posh, ended up somewhere else. In the latter case you may want to search for its location and use that path in the next steps.

3. Open `.profile`:

    ```bash
    sudo nano ~/.profile
    ```

    then comment out the following lines:
    
    ```bash
    # set PATH so it includes user's private bin if it exists
    if [ -d "$HOME/.local/bin" ] ; then
        PATH="$HOME/.local/bin:$PATH"
    fi
    ```

    to match:
    ```bash
    # set PATH so it includes user's private bin if it exists
    #if [ -d "$HOME/.local/bin" ] ; then
    #    PATH="$HOME/.local/bin:$PATH"
    #fi
    ```
    
    close the `.profile` file (`Ctrl`+`O`, `Enter`, and then `Ctrl`+`X`)

4. For user installed applications that live in `$HOME/.local/bin` to be available, `$HOME/.local/bin` should be in the `$PATH` environment variable. Add this guarded block to `.profile` immediately before `# if running bash`:

	```bash
    PROFILE="$HOME/.profile"
    ANCHOR='^# if running bash$'
    MARKER='HOME/.local/bin'

    if ! grep -q "$MARKER" "$PROFILE"; then
        if grep -q "$ANCHOR" "$PROFILE"; then
            sed -i "/$ANCHOR/i\\
    # Set PATH so it includes user's private bin if it exists\\
    if [ -d \"$HOME/.local/bin\" ] && [[ \":$PATH:\" != *\":$HOME/.local/bin:\"* ]]; then\\
      export PATH=\"$HOME/.local/bin:$PATH\"\\
    fi\\
    " "$PROFILE"
        else
            echo "WARNING: anchor line not found in $PROFILE - appending to end instead, check ordering manually" >&2
            printf '\n# Set PATH so it includes user\'s private bin if it exists\nif [ -d "$HOME/.local/bin" ] && [[ ":$PATH:" != *":$HOME/.local/bin:"* ]]; then\n  export PATH="$HOME/.local/bin:$PATH"\nfi\n' >> "$PROFILE"
        fi
    fi
	```

5. Initialize Oh My Posh with a theme. To use Oh My Posh with a theme of your choice (e.g., `atomic`), add the following idempotent initialization command to your `.bashrc` file:
    
    ```bash
    if ! grep -q 'oh-my-posh init bash --config ~/.cache/oh-my-posh/themes/atomic.omp.json' ~/.bashrc; then
        echo -e "\n# Use Oh My Posh with atomic theme" >> ~/.bashrc
        echo 'eval "$(oh-my-posh init bash --config ~/.cache/oh-my-posh/themes/atomic.omp.json)"' >> ~/.bashrc
    fi
    ```
    
6. Reload the shell for the changes to take effect:
    
    ```bash
    source ~/.bashrc
    ```

7. Check the install using:

    ```bash
    oh-my-posh --version
    ```

That's it! You should now have an appealing Bash prompt with Oh My Posh.

## Upgrading Oh My Posh

Having installed Oh My Posh manually, we don't automatically get upgrade notifications. Therefore, to see if a new version is available run:

```bash
oh-my-posh notice
```

Upgrading Oh My Posh manually using the `upgrade` command is simple:

```bash
oh-my-posh upgrade
```

To enable automated upgrades, run:

```bash
oh-my-posh enable upgrade
```

The above command will modify the config file and as new version becomes available Oh My Posh will be upgraded.

## "Standalone" Linux Distribution

If running a Linux distro as the principal OS, so outside WSL and not using Windows Terminal, then Oh My Posh requires a Nerd font installed within Linux. A Nerd font includes extra glyphs that are shown in the prompt. You can install a Nerd font using the following command:

```bash
oh-my-posh font install
```
    
This command will open an interactive menu. Scroll to select your preferred font and confirm. Personally, I recommend the `Hack Nerd Font`.

<a href="../README.md">Back to README</a>