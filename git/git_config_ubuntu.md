<a href="../README.md">Back to README</a>

# Git on WSL Ubuntu

## General Notes and Considerations

Since these instructions concern installing and configuring Git as part of my development environment, I assume that the same SSH-key pairs used on the Windows side will also be used in WSL 2 Ubuntu. For this, the SSH key pair is saved in a OneDrive directory, which is located on the Windows side. If you created a password-protected SSH key pair, see the note at the end of this document.

You might also want to look at [Get started using Git on Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git).

## Make Git Updatable on Ubuntu on WSL 2

I was working with Git on Ubuntu on WSL 2 and noticed that my Git version was outdated. To work with the latest Git release, I needed to update it.

### The Problem

Ubuntu on WSL 2 comes with Git pre-installed, but the version is often outdated. So, how do you update Git in WSL 2 Ubuntu?

### The Solution

To ensure Git can be updated with the latest releases, we need to add the Git PPA (Personal Package Archive) to our system.

1. Add the PPA. Add the Git PPA to your system with the following command:
    
    ```bash
    sudo add-apt-repository ppa:git-core/ppa
    ```

    This adds the PPA to your `/etc/apt/sources.list.d/` directory, creating a file like `git-core-ubuntu-ppa-noble.list`. Note: The filename includes the codename of your current Ubuntu release (e.g., noble for Ubuntu 24.04). This is automatically determined by add-apt-repository, so you don't need to worry about specifying it manually. If you upgrade your Ubuntu version in the future (i.e. replace it in WSL do not upgrade it inside WSL!), re-adding the PPA will generate a new file with the updated codename.
    
2. Update the package list. Update your package list to include the new repository:
    
    ```bash
    sudo apt update
    ```

3. Check that Git is already installed:

    ```bash
    git --version
    ```

    If it is installed proceed to step 5.

4. Install Git if it isn't already installed:
    
    ```bash
    sudo apt install git
    ```

    After installing, proceed to the next section on configuring Git.

5. After adding the PPA (step 1) and running `sudo apt update`, Git should now be upgradable. Run `apt list --upgradable` to see if a new version is available. If so, then upgrade Git to the latest version:
	
	```bash
	sudo apt upgrade git
	```

To manage or remove this PPA in the future, use:

```bash
sudo add-apt-repository --remove ppa:git-core/ppa
```

## Configure Git on Ubuntu

### Name and Email

Instruct Git to use your name and email on your system globally by setting your name:

```bash
git config --global user.name "Your Name"
```

and your email:
   
```bash
git config --global user.email "youremail@domain.com"
```

### Main vs Master

Since GitHub defaults to main instead of master, it is good practice to set the default branch name to main. To check this use:

```bash
git config --global init.defaultBranch
```

If this does not return `main` then set it:

```bash
git config --global init.defaultBranch main
```

### Setting up SSH Key Authentication for Git Repos

Hint: Configuring Git in Linux involves editing configuration files. I use nano for this, a simple text editor. From the command line, a configuration file can be edited with nano by running:

```bash
nano file_to_edit
```

Using the SSH keys saved in Windows (OneDrive) inside WSL Ubuntu:

1. To enable metadata support for proper Linux-style permissions on mounted drives, in `/etc/wsl.conf` add:

    ```text
    [automount]
    enabled  = true
    root     = /mnt/
    options  = "metadata,umask=22,fmask=11"
    ```

    Reboot your machine.

2. Then change the mode of the private key (identity file) since SSH on Linux is not that permissive compared to Windows. Do `chmod 600` on the private key since SSH requires private keys to have restricted permissions:

    ```bash
    sudo chmod 600 /mnt/c/Users/<username>/OneDrive/Documents/ssh_keys/github
    ```

    Make sure to use the correct path to your identity file. Note that the &lt;username&gt; in the path refers to your Windows username.

3. Open the SSH configuration file:

    ```bash
    sudo nano ~/.ssh/config
    ```

    Add the following to `~/.ssh/config`:

    ```text
    Host github_ssh_connection
        HostName github.com
        IdentityFile /mnt/c/Users/<username>/OneDrive/Documents/ssh_keys/github
    ```

    Again, make sure to use the correct path to where your identity file lives. Here, `github_ssh_connection` is a custom alias. You can name it anything, but be consistent when using it in git clone commands.

4. Test the SSH connection (GitHub identity) to GitHub:

    ```bash
    ssh -T git@github_ssh_connection
    ```

5. Now we can use:

    ```bash
    git clone git@github_ssh_connection:<username>/repo.git
    ```

6. To get an overview of the Git configuration use:

    ```bash
    git config --list
    ```

## Optional: Using ssh-agent for Passphrase-Protected Keys

If you created your SSH key pair with a passphrase, you can use ssh-agent to avoid entering it repeatedly. In a Bash terminal run:

```bash
eval "$(ssh-agent -s)"
```

This starts the SSH agent and sets environment variables so your shell can communicate with it. Then, add the private key to the SSH agent:

```bash
ssh-add /mnt/c/Users/<username>/OneDrive/Documents/ssh_keys/github
```

Verify the SSH key is loaded:

```bash
ssh-add -l
```

This adds your key to the agent for the current session. You won't be prompted for the passphrase again until the session ends.

That's it! Git is now configured and ready to use in your WSL 2 Ubuntu environment.

<a href="../README.md">Back to README</a>