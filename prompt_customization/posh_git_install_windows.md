<a href="../README.md">Back to README</a>

# Install posh-git on Windows

These instructions assume you're using PowerShell (version 6 or higher) on Windows 11. This ultra short guide covers the installation of [posh-git](https://github.com/dahlbyk/posh-git) on Windows 11. Configuration of PowerShell and Windows PowerShell to use posh-git is covered in <a href="../powershell/powershell_configure_windows.md">powershell_configure_windows.md</a>.

## Why posh-git?

posh-git is a PowerShell module that integrates Git and PowerShell by providing Git status summary information that can be displayed in the PowerShell prompt. I find it invaluable when working with Git to immediately see the status of the branch I'm working on. posh-git also provides tab completion support for common git commands, branch names, paths and more. 

## Installing posh-git via PowerShellGet

1. Open up an elevated PowerShell prompt: Type PowerShell in the search bar, right-click PowerShell icon and select "Run as administrator".

2. If you've never installed posh-git from the PowerShell Gallery, execute:

    ```powershell
    PowerShellGet\Install-Module posh-git -Scope CurrentUser -Force
    ```

    NOTE: If you're asked to trust packages from the PowerShell Gallery, answer yes to continue installation of posh-git

3. Verify the installation:

    ```powershell
    Get-Module -ListAvailable posh-git
    ```

    To temporarily test the install you can import the package for the current shell session:

    ```powershell
    Import-Module posh-git
    ```

## Updating posh-git via PowerShellGet

If you've installed a previous version of posh-git from the PowerShell Gallery you can update it running:

```powershell
PowerShellGet\Update-Module posh-git
```

<a href="../README.md">Back to README</a>