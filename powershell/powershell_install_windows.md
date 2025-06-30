<a href="../README.md">Back to README</a>

# Cross-Platform PowerShell on Windows

## Why PowerShell?

[Powershell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell), a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration management framework, is the successor of Windows PowerShell (Windows PowerShell). For my development environment I prefer PowerShell over Windows PowerShell because it is cross-platform, and I plan to use it across different environments as my proficiency grows.

## Installing PowerShell

Since Windows comes with Windows PowerShell, you can install [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows) using winget. 

1. From within a Windows PowerShell or a Command Prompt (cmd) terminal:

    ```powershell
    winget search Microsoft.PowerShell
    ```

    from the list, pick the latest non preview version and copy the ID:

2. Install PowerShell using the ID

    ```powershell
    winget install -id Microsoft.PowerShell --source winget
    ```

3. Verify the install with:

    ```powershell
    pwsh --version
    ```

If the installation was successful you can launch PowerShell from the start menu. Once Windows Terminal is installed, I plan to set PowerShell as the default profile.

## Configuring Execution Policy

For other programs like Oh My Posh and posh-git to work, the [execution policy](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy) for the current user (yes, that's you or me) must be set to remote signed. Check this via:

```powershell
Get-ExecutionPolicy -List
```
	
To set it:
	
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```
	
Do the above for both PowerShell and Windows PowerShell because Windows PowerShell is still the default shell in some contexts.

**Note**: RemoteSigned allows local scripts to run freely while requiring downloaded scripts to be signed by a trusted publisher. This balances security with convenience, which is ideal for development setups like this one.

<a href="../README.md">Back to README</a>