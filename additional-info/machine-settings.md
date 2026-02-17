# VS Code Settings Machine (Remote)
```json
{
    // Editor
    "ruff.importStrategy": "useBundled",
    "ruff.configuration": "/path/to/ruff.toml",
    "[python]": {
        // "editor.formatOnSave": true,
        "editor.codeActionsOnSave": {
            "source.fixAll": "explicit",
            "source.organizeImports": "explicit"
        },
        "editor.defaultFormatter": "charliermarsh.ruff"
    },
    // Python
    "python.analysis.autoSearchPaths": true,
    "python.analysis.diagnosticSeverityOverrides": {
        "reportMissingImports": "none"
    },
    "python.analysis.typeCheckingMode": "basic",
    "python.terminal.activateEnvironment": true,
    "python.terminal.activateEnvInCurrentTerminal": true,
    "autoDocstring.docstringFormat": "google-notypes",
    // Jupyter
    "jupyter.interactiveWindow.textEditor.executeSelection": true,
    "jupyter.interactiveWindow.creationMode": "perFile",
}
```