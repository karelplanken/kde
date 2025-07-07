# Viewing Matplotlib Plots Interactively WSL 2 Ubuntu

## The Potential Issue

WSL 2 uses WSLg to display GUI applications, but outdated Mesa drivers can cause rendering issues with matplotlib plots.

If having issues with interactively viewing plots generated with matplotlib (running in Ubuntu and displaying in Windows), then (see: https://github.com/microsoft/wslg/discussions/312 and https://stackoverflow.com/questions/78068008/wsl-matplotlib-artifacts) add mesa repository:

```bash
sudo add-apt-repository ppa:kisak/kisak-mesa
```

and update mesa:

```bash
sudo apt update && sudo apt upgrade
```

Then verify by viewing a plot interactively from within a Python program or script.