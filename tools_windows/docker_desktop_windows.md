<a href="../README.md">Back to README</a>

# Docker Desktop on Windows WSL2 Backend (x64)

The install instructions are taken from the [Docker Docs](https://docs.docker.com/desktop/setup/install/windows-install/) and slightly customized.

## Why Docker Desktop?

This section describes how to install Docker Desktop on Windows 11 using the WSL2 backend. Docker is a core component of this development environment, enabling containerized workflows and consistent dev/test environments. In fact, installing only WSL2 and Docker Desktop would suffice, potentially eliminating the need for Ubuntu and its associated tools and customizations. Since WSL2 is already configured, Docker Desktop will integrate with it to provide a seamless Linux-based container experience on Windows.

## Install Interactively

1. Download the installer from the official [Docker Docs](https://docs.docker.com/desktop/setup/install/windows-install/) site.

2. Double-click `Docker Desktop Installer.exe` to run the installer. By default, Docker Desktop is installed at `C:\Program Files\Docker\Docker`.

3. When prompted, ensure the `Use WSL 2` instead of `Hyper-V` option on the Configuration page is selected.

    On systems that support only one backend, Docker Desktop automatically selects the available option.

4. Follow the instructions on the installation wizard to authorize the installer and proceed with the installation. You may be prompted to reboot the machine.

5. When the installation is successful, select Close to complete the installation process.

6. Start Docker Desktop.

## Install from PowerShell

1. Download the installer:

    ```powershell
    Invoke-WebRequest `
        -Uri "https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe" `
        -Outfile "$HOME\Downloads\Docker_Desktop_Installer.exe"
    ```

2. Run the installer:

    ```powershell
    Start-Process "$HOME\Downloads\Docker_Desktop_Installer.exe" -Wait `
        -ArgumentList 'install', '--accept-license'
    ```

    You may be prompted to reboot the machine.

3. If your admin account is different to your user account, you must add the user to the docker-users group to access features that require higher privileges, such as creating and managing the Hyper-V VM, or using Windows containers. Check that you are in this group:

    ```powershell
    net localgroup docker-users
    ```

    If not then add yourself using:

    ```powershell
    net localgroup docker-users <user> /add
    ```

    Replace `<user>` with your actual Windows username.

4. Check the install with verifying the version number:

    ```powershell
    docker --version
    ```

## Final Note

Finally, you can test if Docker works on your system by pulling the Hello World image:

```powershell
docker run hello-world
```

This should get you an output with something like "Hello from Docker!".

Regardless of the install method you used, you can start Docker Desktop from the Start Menu. Since the Docker Engine might keep running in the background and Docker Desktop might be added to the start group, check the system tray icon when in doubt whether Docker Desktop is up and running.

<a href="../README.md">Back to README</a>