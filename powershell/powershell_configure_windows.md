<a href="../README.md">Back to README</a>

# Configure PowerShell and Windows PowerShell
 
After having installed Oh My Posh and posh-git, PowerShell can be configured to use these programs to customize the prompt for increased productivity and, perhaps more importantly, to make it more readable. Since Windows still comes with Windows PowerShell I tend to configure them both because sometimes I find myself using Windows PowerShell.

The commands in the instructions below can be used in both PowerShell and Windows PowerShell.

## Profile Script File

Both PowerShell and Windows PowerShell have a profile script file named `Microsoft.PowerShell_profile.ps1`. The $PROFILE variable points to the current user's profile script file, which runs every time a new PowerShell session starts.

1. You can create a profile script in one go by running the following in a PowerShell terminal:

    ```powershell
    if (!(Test-Path -Path $PROFILE)) {
        New-Item -ItemType File -Path $PROFILE -Force
    }
    ```
    
2. To see what the condition does, you can run it separately:

    ```powershell
    Test-Path -Path $PROFILE
    ```

    If this returns "True" then it exists, if not proceed to step 3.

3. If step 2 returned "True" then proceed skip the command below, if else it returned ""False", create a profile script file using:

    ```powershell
    New-Item -Path $PROFILE -Type File -Force
    ```

After creating the profile script file you can test its existence with the command given in the step 2. Do the above also for Windows PowerShell.

Note that PowerShell supports multiple profile script scopes (e.g., all users, all hosts). To inspect them:

```powershell
$PROFILE | Select-Object *
```

Setting up the profile script only for the current user aligns with the Principle of Least Privilege and the Security with Usability principle. It ensures that:

- You don't affect other users or system-wide behavior.
- You maintain a secure and personalized configuration.

## Configure PowerShell and Windows PowerShell to Use Oh My Posh

Open the profile script file from within a terminal:

```powershell
notepad $PROFILE
```

and add this to the profile script file:

```powershell
# Use Oh My Posh with the atomic theme if available
if (Get-Command oh-my-posh -ErrorAction SilentlyContinue) {
    oh-my-posh init pwsh `
    --config "$env:POSH_THEMES_PATH\atomic.omp.json" `
    | Invoke-Expression
}
```

Since I have multiple machines that share the same OneDrive the loading/initialization and invoking has to be done conditionally. The line added to the profile script file initializes oh-my-posh (init), sets the theme (--config) and applies the configuration (Invoke-Expression). Loading Oh My Posh unconditionally can be achieved using:

```powershell
# Use Oh My Posh with the atomic theme
oh-my-posh init pwsh `
  --config "$env:POSH_THEMES_PATH/atomic.omp.json" `
  | Invoke-Expression
```

Here I've chosen the atomic theme just because that's my favorite. You can explore other themes by browsing the Oh My Posh themes gallery and updating the `--config` path accordingly.

Instead of adding the lines to the profile script file manually you can also add them from within PowerShell:

```powershell
Add-Content -Path $PROFILE -Value @"
# Use Oh My Posh with the atomic theme if available
if (Get-Command oh-my-posh -ErrorAction SilentlyContinue) {
    oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\atomic.omp.json" | Invoke-Expression
}
"@
```

## Configure PowerShell to Use posh-git

Because posh-git was installed from within PowerShell with PowerShellGet (from the PowerShell Gallery), the module lives in the PowerShell program directory. Therefore, we first configure PowerShell to use posh-git, and then open the profile script file from within a terminal running PowerShell:

```powershell
notepad $PROFILE
```

and add this to the ps file:
	
```powershell
# Enable Git status information and tab completion
Import-Module posh-git
```

Or directly from the command line:

```powershell
Add-Content -Path $PROFILE -Value @"

# Enable Git status information and tab completion
Import-Module posh-git
"@
```

Note that since the posh-git module is installed locally for the current user, i.e. in the directory on Onedrive no conditional loading is required when working with multiple machines using a shared OneDrive.

## Configure Windows PowerShell to Use PowerShell's posh-git Module

1. To use the same posh-git module in Windows PowerShell, create a symbolic link (symlink) in an elevated PowerShell:
	
    ```powershell
    New-Item -ItemType SymbolicLink `
            -Path "C:\Program Files\WindowsPowerShell\Modules\posh-git" `
            -Target "C:\Program Files\PowerShell\Modules\posh-git"
    ```
	
2. Verify the symlink:
	
    ```powershell
    Get-ChildItem "C:\Program Files\WindowsPowerShell\Modules"
    ```

	and get an output showing something like `posh-git` pointing to the PowerShell module.

3. Add the following to the Windows PowerShell profile script (use `$PROFILE` to get its location):

    ```powershell
    Add-Content -Path $PROFILE -Value @"
    # Enable Git status information and tab completion (symlink to PowerShell module)
    Import-Module posh-git
    "@
    ```

    Close and reopen the Windows PowerShell terminal to apply changes. If Windows PowerShell starts without errors everything should be fine.

## Final Check

Make sure everything is working as expected:
- Open PowerShell and confirm the prompt is themed.
- Run `git status` in a repo to see posh-git in action.
- Open Windows PowerShell and confirm the same behavior.

<a href="../README.md">Back to README</a>