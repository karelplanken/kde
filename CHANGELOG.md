# Changelog

## [3.1.0] - 2026-07-11

### Changed

- Updated Ubuntu setup docs to align with WSL2 login shell behavior:

    - prompt-customization/oh-my-posh-install-ubuntu.md
    - tools-ubuntu/uv-install-ubuntu.md

- Replaced `.profile` export append instructions with anchor-based, idempotent insertion before the `# if running bash` block to preserve required startup ordering.
- Kept `.bashrc` interactive setup snippets as append operations, now with idempotency guards for Oh My Posh and uv/uvx completions.
- Added a new reference document:

    - additional-info/profile-vs-bashrc-wsl2.md

- Updated README navigation to insert the new WSL2 intro section before Ubuntu steps for Oh My Posh, Git, and uv.
- Bumped project version from 3.0.0 to 3.1.0 in README and changelog.

## [3.0.0] - 2026-07-10

### Changed

- BREAKING: Split the Windows Terminal guide into separate check-install and configuration documents.
- Updated README.md to the new 3.0.0 release version and current navigation flow.
- Revised the following documentation files as part of the major refresh:

    - additional-info/user-settings.jsonc
    - git/git-install-config-windows.md
    - powershell/powershell-configure-windows.md
    - powershell/powershell-install-windows.md
    - prompt-customization/oh-my-posh-install-windows.md
    - tools-ubuntu/uv-install-ubuntu.md
    - tools-windows/winget-check-install-windows.md
    - tools-windows/wsl-install-windows.md

- Replaced windows-terminal/windows-terminal-install-and-config.md with:

    - windows-terminal/windows-terminal-check-install.md
    - windows-terminal/windows-terminal-config.md

## [2.0.0] - 2026-02-17

### Changed

- BREAKING: Renamed directories and documentation files from underscore style to hyphen style.
- Updated internal links and references across the project to match the new paths.
- Applied typo and wording fixes across key documentation files.

## [1.1.0] - 2025-07-07

### Changed

- Major revisions of:

    - README.md
    - git-config-ubuntu.md
    - git-install-config-windows.md
    - powershell-configure-windows.md
    - oh-my-posh-install-ubuntu.md
    - uv-install-ubuntu.md
    - wsl-install-windows.md

- Minor revisions of:

    - powershell-install-windows.md
    - oh-my-posh-install-windows.md
    - vs-code-install-windows.md
    - windows-terminal-install-and-config.md

Added:

- CHANGELOG.md
- interactive-matplotlib-plots-ubuntu-wsl.md
- wsl2-shell-initialization.md
- winget-check-install-windows.md

General

- Corrected typos and formatting in all Markdown files
- Improved README structure and added badges

## [1.0.0] - 2025-06-01

### Added

- Initial release with core documentation
