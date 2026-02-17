<a href="../README.md">Back to README</a>

# Cross-Platform PowerShell on Windows

## Why PowerShell?

[PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell), a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration management framework, is the successor to Windows PowerShell. For my development environment I prefer PowerShell over Windows PowerShell because it is cross-platform, and I plan to use it across different environments as my proficiency grows.

## Installing PowerShell

Since Windows comes with Windows PowerShell, you can install [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows) using WinGet. 

1. From within a Windows PowerShell or a Command Prompt (cmd) terminal:

    ```powershell
    winget search -e --id Microsoft.PowerShell
    ```

    From the list, pick the latest non-preview version and copy the ID.

2. Install PowerShell using the ID:

    ```powershell
    winget install -e --id Microsoft.PowerShell --source winget
    ```

3. After restarting Windows Terminal, verify the install with:

    ```powershell
    pwsh --version
    ```

    or even better, just start PowerShell and run the same command in there.

If the installation was successful, you can launch PowerShell from the Start menu. Once Windows Terminal is installed, which is probably already the case since Windows 11 comes with Windows Terminal, I plan to set PowerShell as the default profile. I'll come back to that later.

## Configuring Execution Policy

For other programs like Oh My Posh and posh-git to work, the [execution policy](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy) for the current user (yes, that's you or me) must be set to RemoteSigned. Check this via:

```powershell
Get-ExecutionPolicy -List
```
	
To set it:
	
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```
	
Do the above for both PowerShell and Windows PowerShell because Windows PowerShell is still the default shell in some contexts. In my case, a freshly installed Windows 11 Enterprise edition, in Windows PowerShell the execution policy was set to Remote for LocalMachine. If you want to unset the RemoteSigned execution policy, run:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Undefined -Scope LocalMachine
```

Note: The RemoteSigned execution policy allows locally created scripts to run freely, while requiring scripts downloaded from the internet to be signed by a trusted publisher. This strikes a balance between security and convenience, making it ideal for development environments like this one.

Setting the execution policy only for the current user aligns with the Principle of Least Privilege and the Security with Usability principle. It ensures that:

- You don't affect other users or system-wide settings.
- You maintain a secure and personalized configuration.


<a href="../README.md">Back to README</a>