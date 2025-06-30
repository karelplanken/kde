<a href="../README.md">Back to README</a>

# Windows Terminal

## General Notes and Considerations

I use Windows Terminal in my dev setup on Windows with WSL Ubuntu because it allows me to work on the WSL Ubuntu side and Windows side simultaneously. Also, with Windows Terminal I have a sort of unified way of accessing environments besides VS Code. Moreover, I think that with PowerShell, Oh My Posh, and posh-git installed, Windows Terminal rounds it all off nicely.

## Why Windows Terminal?

Windows Terminal is a terminal application for use with command-line tools and shells like Command Prompt, PowerShell, and WSL, i.e. bash. It allows to work with multiple tabs and supports Unicode and UTF-8 characters. Moreover, it can be customized via themes, styles can be set and configured.

## Install Windows Terminal

There are several methods you can install Windows Terminal via the Microsoft Store, from the PowerShell Gallery or using winget:

```powershell
winget install -e --id Microsoft.WindowsTerminal
```

Verify the installation by running Windows Terminal. 

## Configure Windows Terminal

Launch Windows Terminal and set it as default terminal:

`WS`→`Settings`→`Startup`→`Default terminal application`→`Windows Terminal`

Set the installed (Hack) Nerd font as default:

`WS`→`Settings`→`Profiles`→`Defaults`→`Appearance`

Set the `Color scheme`, `Font face`, and `Font size` here. I also set a background image here.

Set the cross-platform PowerShell as the default profile:

`WS`→`Settings`→`Startup`→`Default profile`→`PowerShell`

Additionally, I love the Github Dark color scheme, therefore I've put the definition of it in a separate JSON file, <a href="color_scheme_windows_terminal.json">color_scheme_windows_terminal.json</a>, in this repo. You can copy it from there and paste it in your Windows Terminal JSON file at the appropriate location inside the schemes array (somewhere around line 100). You can open the Windows Terminal JSON file from within settings in the lower left corner.

<a href="../README.md">Back to README</a>