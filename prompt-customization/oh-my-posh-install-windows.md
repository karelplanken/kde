<a href="../README.md">Back to README</a>

# Oh My Posh on Windows

These instructions assume you're using PowerShell on Windows 11. This guide covers the installation of Oh My Posh on Windows 11. Configuration of PowerShell and Windows PowerShell to use Oh My Posh is handled in a separate document.

## Why Oh My Posh?

To make interacting with the cross-platform PowerShell and Windows PowerShell using the terminal nicer and easier to digest, I like to pimp the prompt with [Oh My Posh](https://ohmyposh.dev/). This will also benefit working with Git. Of course you can find all instructions in the docs.

## Installing Oh My Posh

1. Oh My Posh is easily installed using WinGet. Open a PowerShell terminal and run:

    ```powershell
    winget search -e --id JanDeDobbeleer.OhMyPosh --source winget
    ```

    If you get a hit matching your search then install it using:

    ```powershell
    winget install -e --id JanDeDobbeleer.OhMyPosh --source winget
    ```

2. After installing, restart the PowerShell terminal.

3. Ensure that oh-my-posh is included in your user's PATH environment variable. Check this with:

    ```powershell
    'oh-my-posh is ' + (
        ((Get-ChildItem Env:Path).Value -match 'oh-my-posh') ? 'found' : 'not found'
        ) + ' in Path'
    ```

    If oh-my-posh is found, proceed to the next step. If it is not found, then check the location of the oh-my-posh binary first:

    ```powershell
    Get-Command oh-my-posh | Select-Object Source
    ```

    and add it manually:

    ```powershell
    $env:Path += ";<path>\oh-my-posh\bin"
    ```

    Replace <path> with the actual directory where Oh My Posh was installed. On many systems this is in the user scope, e.g. `$HOME\AppData\Local\Programs`. If so then run:

    ```powershell
    $env:Path += ";$HOME\AppData\Local\Programs\oh-my-posh\bin"
    ```

    Depending on package version/manifest and install scope, Oh My Posh may also be installed machine-wide (for example under `C:\Program Files (x86)\oh-my-posh\`). Always verify the actual location on your system with:

    ```powershell
    Get-Command oh-my-posh | Select-Object Source
    ```

    **Notes on Install Location and Theme Paths**

    - Install location can differ across versions and install scope (`user` vs `machine`).
    - If you see a path with a double backslash (for example `themes\\atomic.omp.json`), that is usually escaped path notation and not a separate folder level.
    - For theme selection, avoid hardcoding absolute paths where possible and prefer using `$env:POSH_THEMES_PATH` in your PowerShell profile configuration.

4. Check that Oh My Posh is installed and works:

    ```powershell
    oh-my-posh --version
    ```

5. Oh My Posh requires a Nerd Font to render icons correctly. If you don’t already have one installed, you can use the built-in font installer instead of downloading and installing a Nerd font manually. In an elevated terminal, the font is installed globally, else the font is installed in the user's directory.
   
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