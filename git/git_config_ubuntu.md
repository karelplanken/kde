<a href="../README.md">Back to README</a>

# Git on WSL Ubuntu

## General Notes and Considerations

Since these instructions concern installing and configuring Git as part of my development environment, I assume that the same SSH-key pairs used on the Windows side will also be used in WSL2 Ubuntu. For this the SSH key pair is saved in a OneDrive directory, which obviously is on the Windows side.

Maybe you might also want to look at [Get started using Git on Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git).

## Make Git Updatable on Ubuntu on WSL2

I was working with Git on Ubuntu on WSL2 and noticed that my Git version was outdated. To work with the latest Git release, I needed to update it.

### The Problem

Ubuntu on WSL2 comes with Git pre-installed, but the version is often outdated. So how to update Git in WSL2 Ubuntu?

### The Solution

To ensure Git can be updated with the latest releases, we need to add the Git PPA (Personal Package Archive) to our system.

1. Add the PPA. Add the Git PPA to your system with the following command:
    
    ```bash
    sudo add-apt-repository ppa:git-core/ppa
    ```
    
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

    After installing, proceed to step 6.

5. Upgrade Git to the latest version if it is already installed:
	
	```bash
	sudo apt upgrade git
	```

This process adds the PPA to your `/etc/apt/sources.list.d/` directory, creating a file like `git-core-ubuntu-ppa-jammy.list`.

Note: The filename includes the codename of your current Ubuntu release (e.g., jammy for Ubuntu 22.04). This is automatically determined by add-apt-repository, so you don't need to worry about specifying it manually. If you upgrade your Ubuntu version in the future (i.e. replace it in WSL do not upgrade it inside WSL!), re-adding the PPA will generate a new file with the updated codename.

To manage or remove this PPA in the future, use:

```bash
sudo add-apt-repository --remove ppa:git-core/ppa
```

## Configure Git on Ubuntu

### Main vs Master

Since GitHub defaults to main instead of master, it is good practice to set the default branch name to main. To check this use:

```bash
git config --global init.defaultBranch
```

If this does not return `main` then set it:

```bash
git config --global init.defaultBranch main
```

### Name and Email

Instruct Git to use your name and email on your system globally by setting your name:

```bash
git config --global user.name "Your Name"
```

and your email:
   
```bash
git config --global user.email "youremail@domain.com"
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

    Make sure to use the right path to where your identity file lives. Note that the username in path refers to the Windows username.

3. Add the following to `~/.ssh/config`:

    ```text
    Host github_ssh_connection
        HostName github.com
        IdentityFile /mnt/c/Users/<username>/OneDrive/Documents/ssh_keys/github
    ```

    Again, make sure to use the right path to where your identity file lives. 

4. Test the SSH connection (GitHub identity) to GitHub:

    ```bash
    ssh -T git@github.com
    ```

5. Now we can use:

    ```bash
    git clone git@github_ssh_connection:<username>/repo.git
    ```

6. To get an overview of the Git configuration use:

    ```bash
    git config --list
    ```

<a href="../README.md">Back to README</a>