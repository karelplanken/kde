<a href="../README.md">Back to README</a>

# Windows Terminal

## General Notes and Considerations

I use Windows Terminal in my dev setup on Windows with WSL Ubuntu because it allows me to work on the WSL Ubuntu side and Windows side simultaneously. Also, with Windows Terminal I have a sort of unified way of accessing environments besides VS Code. Moreover, I think that with PowerShell, Oh My Posh, and posh-git installed, Windows Terminal rounds it all off nicely.

## Why Windows Terminal?

Windows Terminal is a terminal application for use with command-line tools and shells like Command Prompt, PowerShell, and WSL, i.e., Bash. It allows you to work with multiple tabs and supports Unicode and UTF-8 characters. Moreover, it can be customized via themes; styles can be set and configured.

## Check that Windows Terminal is Installed

Just like with WingGet, you should already have Windows Terminal since that comes with Windows 11. Check if you have Windows Terminal by running:

```powershell
winget list --id Microsoft.WindowsTerminal
```

If you get output listing a Windows Terminal version then you're all set and you can continue to configure Windows Terminal. If you don't have it then there are several methods you can install Windows Terminal. You can install it via the Microsoft Store, from the PowerShell Gallery or using WinGet:

```powershell
winget install -e --id Microsoft.WindowsTerminal
```

Verify the installation by running Windows Terminal. 

<a href="../README.md">Back to README</a>