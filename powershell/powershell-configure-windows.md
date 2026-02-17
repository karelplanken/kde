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

3. If step 2 returned "True", skip the command below. If it returned "False", create a profile script file using:

    ```powershell
    New-Item -Path $PROFILE -Type File -Force
    ```

After creating the profile script file you can test its existence with the command given in step 2. Do the above also for Windows PowerShell.

Note that PowerShell supports multiple profile script scopes (e.g., all users, all hosts). To inspect them:

```powershell
$PROFILE | Select-Object *
```

Setting up the profile script only for the current user aligns with the Principle of Least Privilege and the Security with Usability principle. It ensures that:

- You don't affect other users or system-wide behavior.
- You maintain a secure and personalized configuration.

## Configure PowerShell and Windows PowerShell to Use Oh My Posh

Note: For Oh My Posh installation details, path variability (`user` vs `machine` scope), and verifying the actual install location on your system, see <a href="../prompt-customization/oh-my-posh-install-windows.md">oh-my-posh-install-windows.md</a>.

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

Note: Because the command below uses a double-quoted here-string (`@" ... "@`), escape `$env:POSH_THEMES_PATH` so it is written literally to your profile and evaluated when the profile runs.

```powershell
Add-Content -Path $PROFILE -Value @"
# Use Oh My Posh with the atomic theme if available
if (Get-Command oh-my-posh -ErrorAction SilentlyContinue) {
    oh-my-posh init pwsh --config "`$env:POSH_THEMES_PATH\atomic.omp.json" | Invoke-Expression
}
"@
```

Alternative (no escaping needed): use a single-quoted here-string so variables are not expanded while writing:

```powershell
Add-Content -Path $PROFILE -Value @'
# Use Oh My Posh with the atomic theme if available
if (Get-Command oh-my-posh -ErrorAction SilentlyContinue) {
    oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\atomic.omp.json" | Invoke-Expression
}
'@
```

## Configure PowerShell to Use posh-git

Because posh-git was installed from within PowerShell with PowerShellGet (from the PowerShell Gallery), the module lives in the PowerShell program directory. Therefore, we first configure PowerShell to use posh-git, and then open the profile script file from within a terminal running PowerShell:

```powershell
notepad $PROFILE
```

and add this to the profile script file:
	
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

Note that since the posh-git module is installed locally for the current user, i.e. in the directory on OneDrive, no conditional loading is required when working with multiple machines using a shared OneDrive.

## Configure Windows PowerShell to Use PowerShell's posh-git Module

To use the PowerShell posh-git module in Windows PowerShell, we can create a symbolic link (symlink) in the Windows PowerShell directory. Because the posh-git module was installed for the current user, it lives in `"$HOME\Documents"`, or in case of a OneDrive setup in the `Documents` directory to which the redirect points. The first steps here are storing the appropriate paths in variables so that the final command is simplified and readable. Open an elevated PowerShell terminal and proceed to the first step.

1.  Get the actual Documents path and store in `$docs`:

    ```powershell
    $docs = [Environment]::GetFolderPath('MyDocuments')
    ```
	
2. Get the path where posh-git is installed to and store in `$source`:
	
    ```powershell
    $source = Split-Path -Parent (Split-Path -Parent (Get-Module -ListAvailable -Name posh-git).Path)
    ```

3. Get the directory in which the symbolic link should be placed, i.e. WindowsPowerShell\Modules, and store in `$target`:

    ```powershell
    $target = Join-Path -Path (Join-Path $docs 'WindowsPowerShell\Modules') -ChildPath 'posh-git'
    ```

    Make sure that the target exists:

    ```powershell
    if (-not (Test-Path -Path $target)) {
        New-Item -ItemType Directory -Path (Split-Path -Parent $target) -Force
    }
    ```

4. Create the symbolic link:

    ```powershell
    New-Item -ItemType SymbolicLink -Path $target -Target $source
    ```

5. Add the following to the Windows PowerShell profile script (use `$PROFILE` to get its location):

    ```powershell
    Add-Content -Path $PROFILE -Value @"

    # Enable Git status information and tab completion (symlink to PowerShell module)
    Import-Module posh-git
    "@
    ```

    Close and reopen the Windows PowerShell terminal to apply changes.

6. If Windows PowerShell starts without errors everything should be fine. You can of course check if the posh-git module is now available for Windows PowerShell:

    ```powershell
    (Get-Module -ListAvailable -Name posh-git).Path
    ```

## Redirected Documents Shortcut Variable

Because my `Documents` directory is redirected from local to the one in OneDrive, changing to it is quite laborious, so I thought I'd create a variable holding the path to the Documents directory on OneDrive. I did this by adding an entry to my profile script:

    ```powershell
    Add-Content -Path $PROFILE -Value @'

    # Variable to cd easily into the redirected Documents on OneDrive
    $docs = [Environment]::GetFolderPath('MyDocuments')
    '@
    ```

Of course you can also consider to set the starting directory in Windows Terminal to this folder, or maybe even do both.

## Final Check

Make sure everything is working as expected:
- Open PowerShell and confirm the prompt is themed.
- Run `git status` in a repo to see posh-git in action.
- Open Windows PowerShell and confirm the same behavior.

<a href="../README.md">Back to README</a>