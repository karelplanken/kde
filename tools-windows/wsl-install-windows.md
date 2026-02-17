<a href="../README.md">Back to README</a>

# WSL on Windows

This short guide is part of my development environment setup on Windows 11, which includes on the Windows side Git, VS Code, PowerShell, Oh My Posh, posh-git, Windows Terminal, and WSL 2. You might want to check out the official [WSL](https://learn.microsoft.com/en-us/windows/wsl/install) installation guide.

## Why WSL

WSL (Windows Subsystem for Linux) allows you to run a full Linux environment directly on Windows without the overhead of a virtual machine. I use WSL because:

- Linux is the standard for development: Many open-source tools and frameworks are built with Linux in mind. Using WSL ensures compatibility and a smoother development experience.
- Access to powerful CLI tools: The Linux command line (especially Bash) offers a rich set of tools that are often more powerful and flexible than their Windows counterparts.
- Performance: Many development tools and build systems run faster on Linux due to better file system performance and native support.
- Seamless integration: WSL 2 offers deep integration with Windows, allowing you to use Linux tools alongside Windows apps, share files, and even run Docker containers natively.
- Consistency across environments: Using WSL helps align your local development environment with production servers, which are often Linux-based.


## Install WSL

Before attempting to install WSL, first check if WSL is already installed by running in PowerShell:

```powershell
wsl --status
```

This command shows whether WSL is installed and what version is set as default. If you already have WSL, you may want to update it:

```powershell
wsl --update
```

### Enable Windows Features: VMP and WSL

Make sure that `Virtual Machine Platform` and `Windows Subsystem for Linux` features are turned on. To check this, click the Start button, type "Windows features", and select "Turn Windows features on or off". You can also check these via the command line, i.e., in a PowerShell terminal:

1. To check if the features are enabled run in an elevated terminal:

    ```powershell
    Get-WindowsOptionalFeature -Online | Where-Object FeatureName -in @("VirtualMachinePlatform", "Microsoft-Windows-Subsystem-Linux")
    ```

    This will return the status of both features. Look for the State property in the output:

    - Enabled means the feature is active.
    - Disabled means it's not currently enabled.

    If not enabled, proceed to the next steps.

2. Enable the `Virtual Machine Platform` feature. In an elevated prompt run:

    ```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform -NoRestart
    ```

3. Enable the `Windows Subsystem for Linux` feature. In an elevated prompt run:

    ```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux -NoRestart
    ```

4. Reboot your machine:

    ```powershell
    Restart-Computer
    ```

Note: Alternatively, use `wsl --install` directly because this command:

- Enables both required features
- Installs the WSL kernel
- Installs Ubuntu by default (you can choose another distro later)

A restart during the WSL install will then be required, however.

### Installing WSL

When installing WSL, the default Linux distribution is Ubuntu. I like Ubuntu so I keep it that way. To install WSL, open an elevated PowerShell prompt (`Run as Administrator`) and execute the following command:
   
```powershell
wsl --install
```
	
Be patient... A reboot may be required during installation if the `Virtual Machine Platform` and `Windows Subsystem for Linux` features were not enabled in advance.

During the install or after the aforementioned reboot, a prompt appears to create a user account and password for the Linux distribution. Note: When entering your password, no characters will appear on screen (this is normal). You'll be prompted to confirm it afterward.

Now that WSL is installed, you can access it from within PowerShell to get all kinds of details about WSL, like the version:

```powershell
wsl --version
```

or the installed distributions with:

```powershell
wsl --list --verbose
```

You can also launch Ubuntu by running `wsl` in PowerShell, from the Start menu, or directly via Windows Terminal.


Hint: Frequently do:

```bash
sudo apt update && sudo apt upgrade
```

to keep your system updated.

## WSL Version

As of now, the default version when installing WSL is likely WSL 2. However, check that this is the case using the above command `wsl --list --verbose`; this should display Ubuntu and version 2. Strangely enough, the version for WSL can only be set after installing it. To set the default version, run in PowerShell:

```powershell
wsl --set-default-version 2
```

This command sets the default WSL version (either 1 or 2) for any new Linux distributions you install after running it. It does not affect already installed distros, nor does it install WSL itself. Moreover, it relies on WSL already being installed and working. The WSL version is set after installing WSL because the command needs the WSL kernel and supporting components to be present. WSL 2 requires a special lightweight VM and a Linux kernel update, which are only available after WSL is installed. So, the logic is:

1. Install WSL (which includes WSL 1 by default).
2. Set WSL 2 as the default for future distros.
3. Optionally convert existing distros to WSL 2 using:

   ```powershell
   wsl --set-version <DistroName> 2
   ```

### Step-by-Step: Ensure Ubuntu is Running on WSL 2

1. Check WSL version support by opening PowerShell as Administrator and running:
   
   ```powershell
   wsl --list --verbose
   ```
   
   This may show something like:
   
   ```powershell
   NAME      STATE           VERSION
   Ubuntu    Running         1
   ```

2. To set WSL 2 as the default version if Ubuntu is running on WSL 1 (as shown in the output under step 1), we can set WSL 2 as the default for future installs:
   
   ```powershell
   wsl --set-default-version 2
   ```

3. Now we can convert the existing Ubuntu WSL 1 instance to Ubuntu WSL 2 with:

   ```powershell
   wsl --set-version Ubuntu 2
   ```

4. Verify after conversion by running:

   ```powershell
   wsl --list --verbose
   ```

   We should now see:
   
   ```powershell
   NAME      STATE           VERSION
   Ubuntu    Running         2
   ```

## Optional: Other Distro

If you wish to install a different distro, then you can add it using:

```powershell
wsl --install -d <DistroName>
```

See available distributions with:

```powershell
wsl --list --online
```

<a href="../README.md">Back to README</a>