<a href="../README.md">Back to README</a>

# Git on Windows

## General Notes and Considerations

I prefer to work with Git using SSH Key-Pair for authentication, so you'll find how to set that up here. Since these instructions concern configuring Git on Windows I assume you're on Windows using PowerShell. Furthermore I assume that you also want to use the same SSH-key pairs from within WSL2 as you do in Windows (this file is part of my development environment setup, which uses WSL2). For this you'll save the SSH key pair in a OneDrive directory, which obviously is on the Windows side.

# Install Git on Windows

When installing Git, particularly if you're not familiar with it, just accept all defaults. Many settings can be changed later and the default values for the install avoid introducing complexity that could make it harder to wrap your mind around how git works. You can dowload the installer from the official [Git](https://git-scm.com/downloads) download site.

Verify that Git is installed by checking its version:

```powershell
git --version
```

## Configure Git on Windows

### Main vs Master

Since GitHub defaults to main instead of master, it is good practice to set the default branch name to main. To check this use:

```powershell
git config --global init.defaultBranch
```

If this does not return `main` then set it:

```powershell
git config --global init.defaultBranch main
```

### Name and Email

Instruct Git to use your name and email on your system globally by setting your name:

```shell
git config --global user.name "Your Name"
```

and your email:
   
```shell
git config --global user.email "youremail@domain.com"
```
   
### Setting up SSH Key Authentication for Git Repos

1. Make sure OpenSSH is installed by inspecting the list in `Settings`→`System`→`Optional features` or:
	
	```shell
	Get-CimInstance win32_service |
	    Where-Object { $_.Name -like 'ssh-agent' } |
	    Select-Object PathName
	```

    If OpenSSH Client is not installed, then install it by adding OpenSSH Client via `System`→`Optional features`→`Add a feature`. 

2. Check that the [SSH configuration file](
    https://superuser.com/questions/1537763/location-of-openssh-configuration-file-on-windows
    ) exists:

    ```powershell
    Test-Path "$HOME\.ssh\config"
    ```

    If the above command returns `False`, then create the configuration file:
    
    ```powershell
    New-Item -Path $HOME\.ssh\config -ItemType File -Force
    ```

3. Generate the SSH key pair:
	
	```shell
	ssh-keygen -t ed25519 -C "description" -f "\path\filename"
	```

	in which:
	 
	- `-t`: Specifies the type of key to create.
	- `-C`: Comment used to identify the SSH key.
	- `-f`: Filename to save the SSH key to.
	
	Now choose for path something like: `$HOME\OneDrive\Documents\ssh_keys\github` with `$HOME` the environment variable pointing to something like `C:\Users\<username>`. PowerShell has built in support for `~`, which works as a shortcut to the home directory. However, combining this with non native commands you'll want to use `$HOME`.
	
    Choose either personal or enterprise OneDrive. If no path is given and only a filename is provided then both files end up in the current working directory. You'll be prompted for a passphrase when running the above command. Just press enter for no password.

4. Copy the output of:
   
	```shell
    cat "$HOME\OneDrive\Documents\ssh_keys\github.pub"
	```

	and paste it in the appropriate field when creating a new SSH key in your GitHub account under `Settings`→`SSH and GPG keys`. Instead of `cat`, which is an alias for `Get-Content` in PowerShell, you can use `Get-Content` directly for clarity. When adding the key to GitHub, it's probably best to use a descriptive title like "Windows Dev Machine" to help identify it later. Note that the key fingerprint will probably be displayed as SHA256. To verify that the local key is the same as the one on GitHub do:
	
	```shell
	ssh-keygen -lf '$HOME\OneDrive\Documents\ssh_keys\github.pub'
	```

	in which:
	
	- `-l`: This stands for "list" and it tells `ssh-keygen` to display the fingerprint of the specified public key file.
	- `-f`: This stands for "file" and it specifies the filename of the public key to be used.

	To specify a different format than the default SHA256, e.g. MD5, use:
		
	```shell
	ssh-keygen -lf $HOME/.ssh/my_ssh_key.pub -E md5
	```
	
	Compare the output to what is displayed on GitHub in your account.

5. Add the following to `"$HOME\.ssh\config"`:
   
	```text
	Host github_ssh_connection
	   HostName github.com
	   IdentityFile ~/OneDrive/Documents/ssh_keys/github
	```

    If your enterprise OneDrive path contains spaces then escape them with '\'.

6. Test the SSH connection to GitHub:

    ```shell
    ssh -T git@github.com
    ```

7. Normally to clone a repo using SSH we do something like:

    ```powershell
    git clone git@github.com:<username>/repo.git
    ```

    Since `"$HOME\.ssh\config"` contains an alias for the host name with the location of the identity file to associate it with the host, we can substitute @github.com: with @github_ssh_connection:

    ```powershell
    git clone git@github_ssh_connection:<username>/repo.git
    ```
<a href="../README.md">Back to README</a>