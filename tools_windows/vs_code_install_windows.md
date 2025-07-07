<a href="../README.md">Back to README</a>

# VS Code on Windows

## General Considerations

This setup is a key part of my development environment. I currently work on Windows 11 in my development environment. If you've followed the installation instructions for this environment you'll have PowerShell, Windows Terminal, WSL 2 with Ubuntu, Oh My Posh, posh-git, and Docker Desktop installed by now. The instructions below finalize the setup of my development environment by adding [VS Code](https://code.visualstudio.com/) that serves as the primary editor, bridging both Windows and WSL environments.

The goal is to have a seamless workflow where I can:
- Develop locally or inside WSL 2 with minimal friction.
- Use consistent tooling across environments.
- Leverage modern Python tools like uv and Ruff for performance and simplicity.
- Integrate Git, Docker, and remote development features directly into my editor.

This guide focuses on installing VS Code, configuring essential extensions, and setting up a modern Python development experience that works well with both Windows and WSL 2.

## Why VS Code

Visual Studio Code is a lightweight, extensible code editor that integrates well with WSL 2, Docker, and modern Python tooling. It supports remote development, has a rich extension ecosystem, and is ideal for working across Windows and Linux environments. In this setup, VS Code serves as the central hub for editing, debugging, and managing both local and remote projects.

## Install VS Code on Windows

Install Visual Studio Code using the Windows Package Manager (`winget`), which provides a streamlined and scriptable way to manage software installations on Windows 11.

1. Verify Package Availability. First, confirm that the VS Code package is available in the `winget` repository:

    ```powershell
    winget search -e --id Microsoft.VisualStudioCode
    ```

    This ensures that the exact package ID is recognized and available for installation.

2. Install VS Code. If the package is listed, proceed with the installation:

    ```powershell
    winget install -e --id Microsoft.VisualStudioCode
    ```

    The `-e` flag ensures an exact match on the package ID, avoiding ambiguity.

3. Restart the terminal running PowerShell.

4. Verify Installation. After installation, confirm that VS Code is correctly installed by checking its version:

    ```powershell
    code --version
    ```

    This should return the installed version number, indicating that the `code` command is available in your system path.

5. You can now start coding from within a PowerShell terminal by running:

    ```powershell
    code .
    ```

    This will open VS Code with the current directory loaded.

## VS Code Extensions

Before installing VS Code extensions, it's important to understand the distinction between local and remote development environments, such as WSL, SSH, or containers, and how VS Code's architecture supports them. This is one of the most common sources of confusion when working with extensions in remote development scenarios.

### Context of VS Code Extensions

VS Code uses a client-server architecture for remote development, which creates two distinct contexts where extensions can run:

1. Local/UI Extensions (Windows side in your WSL setup):    
    These run in the VS Code client and handle user interface, themes, and local functionality. Examples include:

    - Themes and color schemes
    - Icon themes
    - Local file managers
    - Keybinding extensions
    - Some language support that doesn't need server-side processing

2. Remote Extensions (WSL/Linux side):  
    These run on the remote server/environment and need access to the actual codebase, filesystem, and development tools. Examples include:

    - Language servers (Python, Node.js, Go, etc.)
    - Debuggers
    - Linters and formatters
    - Git extensions that interact with repositories
    - Terminal and shell extensions
    - Most development-focused extensions

When you install an extension, VS Code usually tries to be smart about where it should run, but you can see and control this in the Extensions panel. Extensions will show:

- "Install in WSL" button when they need to run remotely
- "Install Locally" when they're UI-focused
- Some extensions can run in both contexts

The key insight is that extensions needing to interact with your code, tools, or filesystem must be installed where those resources actually exist. Extensions focused on VS Code's interface run locally where the UI is rendered.

This is why you might install a Python extension in WSL (where your Python interpreter lives) but a theme extension locally (where the UI is displayed).

[Learn more about VS Code Remote Development](https://code.visualstudio.com/docs/remote/remote-overview).

### VS Code Extensions to Install

To enhance productivity and streamline development across both Windows and WSL environments, I installed the following extensions in VS Code:

1. Windows (Local)  
    These extensions are installed in the Windows instance of VS Code:

    - Remote Development (extension pack)
        Includes:
        - Remote - SSH
        - Remote - Tunnels
        - Dev Containers
        - WSL  
  
        Enabling any of the extensions included in the Remote Development extension pack will activate the Remote Explorer panel in VS Code.

    - Docker    
    Provides integration with Docker Desktop for managing containers and images directly from VS Code.

    - C/C++ Extension Pack
        Includes:
        - C/C++
        - C/C++ Themes
        - CMake Tools

    - Doxygen   
    Documentation generation.

    - PlatformIO    
    Useful for embedded development and working with microcontrollers.

2. WSL:Ubuntu (Remote)  
    These extensions are installed in the WSL 2 Ubuntu environment:

    - Python (extension pack)  
    Required for debugging, IntelliSense (via Pylance), and Jupyter notebook support.

    - Jupyter  
    Enables rich notebook editing and execution inside VS Code.

    - Ruff  
    A modern Python linter and formatter with a built-in language server (`ruff server`).

    - autoDocstring  
    Automatically generates Python docstrings based on function signatures.

### Modern Python Setup with Ruff

Ruff has evolved into more than just a linter. With the introduction of its language server, it now supports:

- Linting
- Formatting
- Import sorting
- Quick fixes

This allows for a leaner setup by replacing traditional tools like `autopep8`, `isort`, `flake8`, and `pylint`.

However, Ruff does not replace the Python extension or Pylance for:

- Debugging
- IntelliSense
- Type checking
- Jupyter support

## Sample `settings.json` for Python Development

Below is a sample `settings.json` configuration for VS Code, tailored for a modern Python development workflow using:

- Ruff (with its language server)
- uv (a fast Python package manager and virtual environment tool that replaces pip and venv)
- Pylance (for IntelliSense and type checking)
- Python extension (for debugging and Jupyter support)

```json
{
  // Python interpreter (optional if uv manages it)
  "python.defaultInterpreterPath": ".venv/bin/python",

  // Use Ruff for linting and formatting
  "ruff.enable": true,
  "ruff.organizeImports": true,
  "ruff.formatOnSave": true,

  // Disable other formatters
  "python.formatting.provider": "none",
  "editor.formatOnSave": true,

  // Enable Pylance for IntelliSense
  "python.languageServer": "Pylance",

  // Optional: Enable type checking
  "python.analysis.typeCheckingMode": "basic",

  // Optional: Exclude virtual environments and build folders
  "files.exclude": {
    "**/__pycache__": true,
    "**/.venv": true,
    "**/build": true,
    "**/dist": true
  },

  // Optional: Ruff-specific settings for Python files
  "[python]": {
    "editor.defaultFormatter": "charliermarsh.ruff"
  }
}
```

### Notes

- Adjust `"python.defaultInterpreterPath"` if you're using `uv` to manage environments outside of `.venv`.
- If you're working in WSL 2, set the interpreter path to the appropriate location inside your WSL distro.
- Ensure that both the Ruff and Python extensions are installed in the appropriate environment (Windows or WSL).

## Conclusion

With VS Code installed and configured, you now have a powerful and flexible development environment that integrates seamlessly with both Windows and WSL 2. By leveraging modern tools like Ruff, uv, and the Remote Development extension pack, you can maintain a clean, efficient workflow across local and remote contexts.

This setup supports:
- Fast and reliable Python development
- Integrated Docker and Git workflows
- Remote editing and debugging in WSL 2
- A consistent experience across environments

As your development needs evolve, VS Code's extensibility allows you to adapt and expand your tooling without disrupting your workflow. This guide provides a solid foundation for building and maintaining a modern, cross-platform development environment.

<a href="../README.md">Back to README</a>