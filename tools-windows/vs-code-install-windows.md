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

## Current (Python) Configuration

The (Python) setup in this environment is maintained in dedicated configuration files, instead of an inline sample `settings.json` in this document.

- Local VS Code user settings (Windows side): <a href="../additional-info/user-settings.jsonc">user-settings.jsonc</a>
- Remote VS Code machine settings (WSL side): <a href="../additional-info/machine-settings.jsonc">machine-settings.jsonc</a>
- Ruff configuration: <a href="../additional-info/ruff.toml">ruff.toml</a>

This reflects the current setup best:

- VS Code local and remote settings are separated by context (Windows UI vs WSL machine).
- Ruff behavior is centrally controlled through `ruff.toml` and referenced from remote settings.
- Python formatting, linting, and code actions are aligned with the Ruff + Pylance workflow described above.

If you adopt this setup, update any placeholder paths in the referenced files (for example, the Ruff config path in remote settings) to match your system.

### Python REPL + Oh My Posh in VS Code Terminal

When using Oh My Posh with a multi-line prompt (for example `atomic`) in VS Code's integrated terminal, pressing `Ctrl+L` in Python REPL sessions can cause redraw issues where the Python prompt (`>>>`) appears behind prompt lines.

In this setup, the following local setting is intentional and used as a practical workaround:

```json
"terminal.integrated.shellIntegration.enabled": false
```

Disabling shell integration makes the VS Code terminal behave more like a standard terminal emulator for this specific workflow. In my setup, Windows Terminal does not show this redraw issue under the same conditions.

Shell integration can still be useful in other workflows, so treat this as a setup-specific choice rather than a universal recommendation.

Source/discussion: [Suddenly REPL in vscode becomes weird](https://discourse.julialang.org/t/suddenly-repl-in-vscode-becomes-weird/85459/4)

Note: Behavior in VS Code's integrated terminal (prompt rendering, clear-screen behavior, shell integration features) can vary by shell, prompt theme, and extension combination. Keep terminal-related settings in local user settings and adjust them only if you encounter issues in your own setup.

## Conclusion

With VS Code installed and configured, you now have a powerful and flexible development environment that integrates seamlessly with both Windows and WSL 2. By leveraging modern tools like Ruff, uv, and the Remote Development extension pack, you can maintain a clean, efficient workflow across local and remote contexts.

This setup supports:
- Fast and reliable Python development
- Integrated Docker and Git workflows
- Remote editing and debugging in WSL 2
- A consistent experience across environments

As your development needs evolve, VS Code's extensibility allows you to adapt and expand your tooling without disrupting your workflow. This guide provides a solid foundation for building and maintaining a modern, cross-platform development environment.

<a href="../README.md">Back to README</a>