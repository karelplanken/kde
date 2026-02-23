![Version](https://img.shields.io/badge/version-2.0.0-brightgreen)
![GitHub last commit](https://img.shields.io/github/last-commit/karelplanken/kde?color=blue)
![GitHub repo size](https://img.shields.io/github/repo-size/karelplanken/kde?color=orange)
![GitHub issues](https://img.shields.io/github/issues/karelplanken/kde?color=yellow)
![GitHub pull requests](https://img.shields.io/github/issues-pr/karelplanken/kde?color=lightgrey)
![License](https://img.shields.io/github/license/karelplanken/kde?color=success)
![Tech Stack](https://img.shields.io/badge/Made%20with-Markdown-blueviolet)

# Karel's Development Environment (KDE)

## Introduction

This document outlines the complete setup of my development environment on a Windows 11 machine (x64) using KDE and WSL 2. It serves as a step-by-step guide for installing and configuring the tools I use regularly.

My workflow spans multiple languages, primarily Python, JavaScript, and C/C++—with the latter two focused on embedded development for platforms like Arduino and Raspberry Pi. In addition to the programming languages I also use my setup to write in markdown, HTML, and CSS.

The system runs Windows 11 with Windows Subsystem for Linux 2 (WSL 2), using the default Ubuntu distribution (though I still think it should've been called Linux Subsystem for Windows, but I digress...).

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

The software components are listed in the order they should be installed. The only prerequisite is a working installation of Windows 11. No prior experience with the tools is assumed. Since WSL 2 is installed halfway, the first part takes place on the Windows side.

Please pay close attention to whether a step applies to Windows or Linux. To keep things organized, detailed installation and configuration instructions are provided in separate files. This avoids overwhelming the reader with a long, monolithic list and makes the setup easier to follow.

### Repo Structure

This is the directory structure sorting the files of this repo:

```text
├── CHANGELOG.md
├── LICENSE
├── README.md
├── additional-info
│   ├── interactive-matplotlib-plots-ubuntu-wsl.md
│   └── wsl2-shell-initialization.md
├── git
│   ├── git-config-ubuntu.md
│   └── git-install-config-windows.md
├── powershell
│   ├── powershell-configure-windows.md
│   └── powershell-install-windows.md
├── prompt-customization
│   ├── oh-my-posh-install-ubuntu.md
│   ├── oh-my-posh-install-windows.md
│   └── posh-git-install-windows.md
├── tools-ubuntu
│   ├── collection-of-tools.md
│   └── uv-install-ubuntu.md
├── tools-windows
│   ├── docker-desktop-install-windows.md
│   ├── vs-code-install-windows.md
│   ├── winget-check-install-windows.md
│   └── wsl-install-windows.md
└── windows-terminal
    ├── color-scheme-windows-terminal.json
    └── windows-terminal-install-and-config.md
```

In principle, all files are accessible from the list below and from each file there's a link back to the list.

## Installing the Software

### Windows 11:

1. <a href="./tools-windows/winget-check-install-windows.md">Check/Install WinGet</a>
2. <a href="./powershell/powershell-install-windows.md">Install PowerShell (cross-platform)</a>
3. <a href="./git/git-install-config-windows.md">Install and configure Git</a>
4. <a href="./prompt-customization/oh-my-posh-install-windows.md">Install Oh My Posh</a>
5. <a href="./prompt-customization/posh-git-install-windows.md">Install posh-git</a>
6. <a href="./powershell/powershell-configure-windows.md">Configure PowerShell and Windows PowerShell</a>
7. <a href="./windows-terminal/windows-terminal-install-and-config.md">Install and configure Windows Terminal</a>
8. <a href="./tools-windows/wsl-install-windows.md">Install WSL Ubuntu</a>

### Ubuntu on WSL 2:
9. <a href="./prompt-customization/oh-my-posh-install-ubuntu.md">Install Oh My Posh</a>
10. <a href="./git/git-config-ubuntu.md">Configure Git</a>
11. <a href="./tools-ubuntu/uv-install-ubuntu.md">Install uv</a>

### Optional on Ubuntu on WSL 2

12. <a href="./tools-ubuntu/collection-of-tools.md">Optional Tools: SQLite3, Cmatrix, Fastfetch, Cowsay, Fortune, etc.</a>

### Windows 11:

13. <a href="./tools-windows/docker-desktop-install-windows.md">Install Docker Desktop</a>
14. <a href="./tools-windows/vs-code-install-windows.md">Install VS Code and extensions</a>

### Optional on Windows 11

- [MySQL Workbench](https://www.mysql.com/products/workbench/) (see official website for install instructions)
- [DB Browser for SQLite](https://sqlitebrowser.org/) (see official website for install instructions)

## What You'll Have After Setup

By the end of this guide, you'll have:
- A fully configured cross-platform dev environment (Windows + WSL 2)
- Git with SSH authentication across Windows and WSL
- A customized terminal with Oh My Posh and posh-git
- Docker, VS Code, and a suite of optional tools for productivity and fun

## Additional Info

In the files below you'll find some additional info on certain topics and potential issues with components in this setup that I removed from the instructions to keep the focus on installation and configuration.

- <a href="./additional-info/interactive-matplotlib-plots-ubuntu-wsl.md">Viewing Matplotlib Plots Interactively WSL 2 Ubuntu</a>
- <a href="./additional-info/wsl2-shell-initialization.md">WSL 2 Ubuntu Shell Initialization</a>

## Project Info

- <a href="./CHANGELOG.md">Changelog</a>
- <a href="#license">License</a>

## License

[![CC0 1.0][cc0-shield]][cc0]

This work is dedicated to the public domain under the [Creative Commons CC0 1.0 Universal (Public Domain Dedication)][cc0].

[cc0]: https://creativecommons.org/publicdomain/zero/1.0/
[cc0-shield]: https://licensebuttons.net/p/mark/1.0/88x31.png
