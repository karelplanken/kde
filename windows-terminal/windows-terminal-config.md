<a href="../README.md">Back to README</a>

# Configuring Windows Terminal

Now that Oh My Posh, posh-git, and PowerShell are installed and configured, let's configure Windows Terminal. The configuration of Windows Terminal is can be done via the GUI or via a JSON file. Below are some directions to configure Windows Terminal via the GUI. If you prefer, you can also open the JSON file from within Windows Terminal settings in the lower left corner.

## Configure Windows Terminal

Launch Windows Terminal (`WT`) and set it as default terminal:

`WT`→`Settings`→`Startup`→`Default terminal application`→`Windows Terminal`

Set the installed (Hack) Nerd font as default:

`WT`→`Settings`→`Profiles`→`Defaults`→`Appearance`

Set the `Color scheme`, `Font face`, and `Font size` here. I also set a background image here.

Set the cross-platform PowerShell as the default profile:

`WT`→`Settings`→`Startup`→`Default profile`→`PowerShell`

Additionally, I love the GitHub Dark color scheme, therefore I've put the definition of it in a separate JSON file, <a href="color-scheme-windows-terminal.json">color-scheme-windows-terminal.json</a>, in this repo. You can copy it from there and paste it in your Windows Terminal JSON file at the appropriate location inside the schemes array (somewhere around line 100). You can open the Windows Terminal JSON file from within settings in the lower left corner.

<a href="../README.md">Back to README</a>