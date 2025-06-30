# Karel's Development Environment (KDE)

## Introduction

This document outlines the complete setup of my development environment on a Windows 11 machine (x64) using KDE and WSL2. It serves as a step-by-step guide for installing and configuring the tools I use regularly.

My workflow spans multiple languages, primarily Python, JavaScript, and C/C++—with the latter two focused on embedded development for platforms like Arduino and Raspberry Pi. In addition to the programming languages I also use my setup to write in markdown, HTML, and CSS.

The system runs Windows 11 with Windows Subsystem for Linux 2 (WSL2), using the default Ubuntu distribution (though I still think it should've been called Linux Subsystem for Windows, but I digress...).

## Disclaimer

Note that I use Windows 11 and various software (among others FOSS), and that I use OneDrive (enterprise) to which I have redirected my Documents folder. Microsoft advises against this but as far as I know and have experienced I see no harm in doing so. All installations and software reported here are at your own risk. I do hope, however, that this repo contributes to your understanding, workflow, productivity, and above all to you having fun working with your system.

What I report here and what I've learned so far is not by any means work of my own. Instead, I learn from other bright people. Concerning this project, here's a not-so-extensive and probably very incomplete list of people that inspired me with whom I could not have achieved the setup for my development environment I have as it is today is:

- Scott Hanselman
- Corey M Schafer
- Abstract programmer
- Dave Ebbelaar
- Konstantin Lübeck (k0nze)
- All people who worked on the documentation of the software mentioned here
- many more...

## How to Use This Guide

The software components are listed in the order they should be installed. The only prerequisite is a working installation of Windows 11. No prior experience with the tools is assumed. Since WSL2 is installed halfway, the first part takes place on the Windows side.

Please pay close attention to whether a step applies to Windows or Linux. To keep things organized, detailed installation and configuration instructions are provided in separate files. This avoids overwhelming the reader with a long, monolithic list and makes the setup easier to follow.

### Repo Structure

This is the directory structure sorting the files of this repo:

```text
│   README.md
│
├───git
│       git_config_ubuntu.md
│       git_install_config_windows.md
│
├───powershell
│       powershell_configure_windows.md
│       powershell_install_windows.md
│
├───prompt_customization
│       oh_my_posh_install_ubuntu.md
│       oh_my_posh_install_windows.md
│       posh_git_install_windows.md
│
├───tools_ubuntu
│       collection_of_tools.md
│       uv_install_ubuntu.md
│
├───tools_windows
│       docker_desktop_windows.md
│       vs_code_install_windows.md
│       wsl_install_windows.md
│
└───windows_terminal
        color_scheme_windows_terminal.json
        windows_terminal_install_and_config.md
```

In principle, all files are accessible from the list below and from each file there's a link back to the list.

## Installing the Software

### Windows 11:

1. <a href="./powershell/powershell_install_windows.md">Install Powershell (cross-platform)</a>
2. <a href="./git/git_install_config_windows.md">Install and configure Git</a>
3. <a href="./prompt_customization/oh_my_posh_install_windows.md">Install Oh My Posh</a>
4. <a href="./prompt_customization/posh_git_install_windows.md">Install posh-git</a>
5. <a href="./powershell/powershell_configure_windows.md">Configure PowerShell and Windows PowerShell</a>
6. <a href="./windows_terminal/windows_terminal_install_and_config.md">Install and configure Windows Terminal</a>
7. <a href="./tools_windows/wsl_install_windows.md">Install WSL Ubuntu</a>

### Ubuntu on WSL2:
8. <a href="./prompt_customization/oh_my_posh_install_ubuntu.md">Install Oh My Posh</a>
9. <a href="./git/git_config_ubuntu.md">Configure Git</a>
10. <a href="./tools_ubuntu/uv_install_ubuntu.md">Install uv</a>

### Optional on Ubuntu on WSL2

- <a href="./tools_ubuntu/collection_of_tools.md">Optional Tools: sqlite3, cmatrix, neofetch, cowsay, fortune, etc.</a>

### Windows 11:

11. <a href="./tools_windows/docker_desktop_windows.md">Install Docker Desktop</a>
12. <a href="./tools_windows/vs_code_install_windows.md">Install VS Code and extensions</a>

### Optional on Windows 11

- [MySQL Workbench](https://www.mysql.com/products/workbench/) (see official website for install instructions)
- [DB Browser for SQLite](https://sqlitebrowser.org/) (see official website for install instructions)

## What You'll Have After Setup

By the end of this guide, you'll have:
- A fully configured cross-platform dev environment (Windows + WSL2)
- Git with SSH authentication across Windows and WSL
- A customized terminal with Oh My Posh and posh-git
- Docker, VS Code, and a suite of optional tools for productivity and fun

## Potential Issues

If having issues with interactively viewing plots generated with matplotlib (running in Ubuntu and displaying in Windows), then (see: https://github.com/microsoft/wslg/discussions/312 and https://stackoverflow.com/questions/78068008/wsl-matplotlib-artifacts) add mesa repository:

```bash
sudo add-apt-repository ppa:kisak/kisak-mesa
```

and update mesa:

```bash
sudo apt update && sudo apt upgrade
```

## License

[![CC0 1.0][cc0-shield]][cc0]

This work is dedicated to the public domain under the [Creative Commons CC0 1.0 Universal (Public Domain Dedication)][cc0].

[cc0]: https://creativecommons.org/publicdomain/zero/1.0/
[cc0-shield]: https://licensebuttons.net/p/mark/1.0/88x31.png
