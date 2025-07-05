<a href="../README.md">Back to README</a>

# WinGet

## General Considerations

[WinGet](https://learn.microsoft.com/en-us/windows/package-manager/winget/) is a command line tool enabling users to discover, install, upgrade, remove and configure applications on Windows 10, Windows 11, and Windows Server 2025 computers. This tool is the client interface to the Windows Package Manager service.

## Why WinGet

I use winget because it comes with Windows 11 and I find it convenient because I don't have to leave the terminal. From within the terminal I can install, update, and remove whatever program I want.

## Check if WinGet is Available

On Windows 11, the Windows Package Manager (winget) is included by default starting with version 21H2 (build 22000) and later. winget might not be available if:

1. You're using a corporate or enterprise-managed device with restrictions.
2. You're on a custom Windows image where optional features were removed.
3. The App Installer is missing or outdated.

To check if winget is available we can do a version check. Open a Windows PowerShell terminal by typing in the search bar "Windows Powershell" and press Windows PowerShell. Run the following command in Windows PowerShell to check if winget is installed (run means here: type and hit enter):

```powershell
winget --version
```

If you get a version number you have winget. If you get something like `winget : The term 'winget' is not recognized as...` then you probably don't have winget.

## Install WinGet

The easiest way to install WinGet is to install App Installer from the Microsoft Store. If installation via Microsoft Store fails, ensure your system is updated and that the Microsoft Store is functioning properly.

<a href="../README.md">Back to README</a>