<a href="../README.md">Back to README</a>

# Oh My Posh on Ubuntu

To enhance the terminal experience and improve readability, I customize the Bash prompt using [Oh My Posh](https://ohmyposh.dev/). This will also benefit working with Git. Of course you can find all instructions in the official docs.

## General Notes and Considerations

This short guide is part of my dev setup for Windows with WSL2 and assumes you have already installed PowerShell, Windows Terminal, and WSL2 with Ubuntu. On my system, Ubuntu is accessed through either Windows Terminal or the integrated terminal in VS Code. Therefore the installation of Oh My Posh in WSL Ubuntu doesn't require a specific Nerd font to be available within Ubuntu.

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

Note: Except for AArch64/ARM64, Oh My Posh can be installed using Homebrew. However, Oh My Posh installed with Homebrew may cause issues after upgrading, such as the terminal becoming unresponsive and displaying errors about missing previous versions. To avoid these issues, I recommend installing Oh My Posh manually using the shell script.

1. Install Oh My Posh:

    ```bash
    curl -s https://ohmyposh.dev/install.sh | bash -s
    ```
    
2. Add Alias for `oh-my-posh`. I assume here that `oh-my-posh` ended up in `~/.local/bin` and `~/.local/bin` is not in `PATH` if the `bash` shell is started in a terminal. To get things right I add an alias to `.bashrc`:

	```bash
	echo -e "\n# Add alias to access oh-my-posh on launch" >> ~/.bashrc && \
        echo "alias oh-my-posh='~/.local/bin/oh-my-posh'" >> ~/.bashrc
	```
	
	Now test it:

	```bash
	exec bash
	```

    Note: If `~/.local/bin` is not in your `PATH`, you may not be able to run `oh-my-posh` directly. Adding an alias ensures it’s accessible in every shell session.

3. Initialize Oh My Posh with a Theme. To use Oh My Posh with a theme of your choice (e.g., `atomic`), add the following initialization command to your `.bashrc` file for interactive, non-login shells:
    
    ```bash
    echo -e "\n# Use Oh My Posh with atomic theme" >> ~/.bashrc && \
    echo 'eval "$(oh-my-posh init bash --config ~/.cache/oh-my-posh/themes/atomic.omp.json)"' >> ~/.bashrc
    ```
    
4. Enable Oh My Posh for login shells. Since `.profile` contains:

	```bash
	# if running bash
	if [ -n "$BASH_VERSION" ]; then
	    # include .bashrc if it exists
	    if [ -f "$HOME/.bashrc" ]; then
	        . "$HOME/.bashrc"
	    fi
	fi
	```

	Oh My Posh is enabled for login shells. Check if this is the case using:

	```bash
	less ~/.profile
	```

	If you don't see these lines then add them.
	
5. Reload the shell. Finally, reload your shell for the changes to take effect:
    
    ```bash
    exec bash
    ```

6. Check the install using:

    ```bash
    oh-my-posh --version
    ```

That's it! You should now have an appealing Bash prompt with Oh My Posh.

## Upgrading Oh My Posh

### Manually upgrading Oh My Posh

Upgrading Oh My Posh manually using the `upgrade` command is simple:

```bash
oh-my-posh upgrade
```

### Automatically Upgrading Oh My Posh

To automatically upgrade Oh My Posh, create a configuration file first:

```bash
oh-my-posh config export --output ~/.mytheme.omp.json
```
       
Add the following to the configuration file:
    
```json
{
    "upgrade": {
    "notice": true,
    "interval": "24h",
    "auto": false,
    "source": "cdn"
    }
}
```

Set "auto" to true to automatically update. The above configuration will trigger a notice that an update is available. You can adjust the lines shown above manually in `~/.mytheme.omp.json` using `nano`:

```bash
nano ~/.mytheme.omp.json
```

Or you can add the contents from within the terminal, for this first install `jq`:

```bash
sudo apt install jq
```

then add using:

```bash
jq '.upgrade = {
    "notice": true,
    "interval": "24h",
    "auto": auto,
    "source": "cdn"
}' ~/.mytheme.omp.json > tmp.json && mv tmp.json ~/.mytheme.omp.json
```

Verify that is has been added using:

```bash
less ~/.mytheme.omp.json
```

Inspect the output and press `q` to exit.

## "Standalone" Linux Distribution

If running a Linux distro as the principal OS, so outside WSL and not using Windows Terminal, then Oh My Posh requires a Nerd font installed within Linux. A Nerd font includes extra glyphs that are shown in the prompt. You can install a Nerd font using the following command:

```bash
oh-my-posh font install
```
    
This command will open an interactive menu. Scroll to select your preferred font and confirm. Personally, I recommend the `Hack Nerd Font`.

<a href="../README.md">Back to README</a>