<a href="../README.md">Back to README</a>

# Oh My Posh on Windows

These instructions assume you're using PowerShell on Windows 11. This guide covers the installation of Oh My Posh on Windows 11. Configuration of PowerShell and Windows PowerShell to use Oh My Posh is handled in a separate document.

## Why Oh My Posh?

To make working in the terminal - both cross-platform PowerShell and Windows PowerShell - nicer and easier to read, I like to pimp the prompt with [Oh My Posh](https://ohmyposh.dev/). This also improves the experience of working with Git. Full documentation is available at the link above.

## Installing Oh My Posh

1. Oh My Posh is easily installed using WinGet. Open a PowerShell terminal and run:

    ```powershell
    winget search -e --id JanDeDobbeleer.OhMyPosh --source winget
    ```

    If you get a hit matching your search then install it using:

    ```powershell
    winget install -e --id JanDeDobbeleer.OhMyPosh --source winget
    ```

2. After installing, you may have to restart the PowerShell terminal.

3. Verify that oh-my-posh is resolvable from PowerShell:

    ```powershell
    Get-Command oh-my-posh -ErrorAction SilentlyContinue | Select-Object Source
    ```

    If this returns a `Source` path, Oh My Posh is correctly on your PATH - proceed to the next step.
    In most cases this resolves to the WindowsApps App Execution Alias folder, e.g.
    `$HOME\AppData\Local\Microsoft\WindowsApps\oh-my-posh.exe`, which is on PATH by default for every
    user account, so no further action is needed.

    If the command returns nothing, first restart the terminal (a fresh session picks up PATH changes
    made by the installer). If it's still not found, locate the actual install directory - depending on
    package version and install scope it may instead live machine-wide, e.g. under
    `C:\Program Files (x86)\oh-my-posh\`. Check with:

    ```powershell
    Get-ChildItem "$env:LOCALAPPDATA\Programs\oh-my-posh" -Recurse -Filter oh-my-posh.exe -ErrorAction SilentlyContinue
    Get-ChildItem "C:\Program Files (x86)\oh-my-posh" -Recurse -Filter oh-my-posh.exe -ErrorAction SilentlyContinue
    ```

    Once you've found it, add it to your **user** PATH persistently (not just the current session):

    ```powershell
    [Environment]::SetEnvironmentVariable(
        'Path',
        [Environment]::GetEnvironmentVariable('Path', 'User') + ';<path-to-directory>',
        'User'
    )
    ```

    Replace `<path-to-directory>` with the actual folder containing `oh-my-posh.exe`. Then open a new terminal and re-run the `Get-Command` check.

    **Notes on Install Location and Theme Paths**

    - Install location can differ across versions and install scope (`user` vs `machine`).
    - For theme selection, avoid hardcoding absolute paths in your PowerShell profile configuration.

4. Check that Oh My Posh is installed and works:

    ```powershell
    oh-my-posh --version
    ```

5. Oh My Posh requires a Nerd Font to render icons correctly. If you don't already have one installed, you can use the built-in font installer instead of downloading and installing a Nerd font manually. In an elevated terminal, the font is installed globally, else the font is installed in the user's directory.

    ```powershell
    oh-my-posh font install
    ```

    This opens an interactive menu. I recommend selecting [Hack Nerd Font](https://www.nerdfonts.com/font-downloads).

## Updating Oh My Posh

You can easily update Oh My Posh using WinGet:

```powershell
winget upgrade JanDeDobbeleer.OhMyPosh -s winget
```

Or maybe even easier:

```powershell
oh-my-posh upgrade
```

## Font Rendering in Windows Terminal and WSL 2

Nerd Fonts only need to be installed on the Windows host system, not inside WSL 2. This is because font rendering is handled by the terminal emulator, e.g., Windows Terminal or VS Code, which runs on Windows.

<a href="../README.md">Back to README</a>
