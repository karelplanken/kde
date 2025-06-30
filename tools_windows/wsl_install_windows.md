<a href="../README.md">Back to README</a>

# WSL on Windows

This ultra short guide is part of my development environment setup on Windows 11, which includes on the Windows side Git, VS Code, PowerShell, Oh My Posh, posh-git, Windows Terminal, and WSL2. You might want to check out the official [WSL](https://learn.microsoft.com/en-us/windows/wsl/install) installation guide.

## Why WSL

WSL (Windows Subsystem for Linux) allows you to run a full Linux environment directly on Windows without the overhead of a virtual machine. I use WSL because:

- Linux is the standard for development: Many open-source tools and frameworks are built with Linux in mind. Using WSL ensures compatibility and a smoother development experience.
- Access to powerful CLI tools: The Linux command line (especially Bash) offers a rich set of tools that are often more powerful and flexible than their Windows counterparts.
- Performance: Many development tools and build systems run faster on Linux due to better file system performance and native support.
- Seamless integration: WSL2 offers deep integration with Windows, allowing you to use Linux tools alongside Windows apps, share files, and even run Docker containers natively.
- Consistency across environments: Using WSL helps align your local development environment with production servers, which are often Linux-based.

## Install WSL

Make sure that `Virtual Machine Platform` and `Windows Subsystem for Linux` features are turned on. To check this, click the Start button, type "windows features", and select "Turn Windows features on or off". The default WSL version is probably 2, but you can set it using:

```powershell
wsl --set-default-version 2
```

When installing WSL, the default Linux distribution is Ubuntu. I like Ubuntu so I keep it that way. To install WSL, open an elevated PowerShell prompt (Run as Administrator) and execute the following command:
   
```powershell
wsl --install
```
	
and be patient... After installing, you'll see that a reboot is required for the changes to take effect.

Once WSL is installed, you can start Ubuntu by typing `ubuntu` in PowerShell or from the Start menu. After boot, a prompt appears to create a user account and password for the Linux distribution. Note that when entering a password you'll type blindly, and fortunately you'll be asked to confirm the password entered.

You can now access from within Windows Terminal. Check for example the WSL version with:

```powershell
wsl --version
```

or the installed distributions with:

```powershell
wsl --list --verbose
```

Hint: Frequently do:

```bash
sudo apt update && sudo apt upgrade
```

to keep your system updated.

## Optional: Other Distro

If you wish to install a different distro then you can add it using:

```powershell
wsl --install -d <DistroName>
```

See available distributions with:

```powershell
wsl --list --online
```

<a href="../README.md">Back to README</a>