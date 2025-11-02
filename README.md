# UMU-Context-Menu Setup
Setup UMU launching from context menu for Windows app in Ubuntu

## Instructions:

Run:

```
mkdir -p ~/.local/bin
nano ~/.local/bin/umu-launcher.sh
```

Paste this:

```
#!/bin/bash
# --- UMU Launcher Wrapper for ZorinOS ---
# Ensures the .exe path is absolute and safe for UMU.

if [ -z "$1" ]; then
  echo "Usage: umu-launcher.sh <path-to-exe>"
  exit 1
fi

exe_path="$(realpath "$1")"

if [ ! -f "$exe_path" ]; then
  echo "Error: file not found at $exe_path"
  exit 1
fi

# Launch using native UMU
exec /usr/bin/umu-run "$exe_path"
```

Then make it executable:

```
chmod +x ~/.local/bin/umu-launcher.sh
```

Now edit the desktop entry that Zorin shows as “Run Windows App with UMU”:

```
nano ~/.local/share/applications/umu-run-exe.desktop
```

Add this (Point to correct exec path):

```
[Desktop Entry]
Name=Run Windows App with UMU
Comment=Run Windows programs using UMU Launcher
Exec=/home/hamzah/.local/bin/umu-launcher.sh %f
Terminal=false
Type=Application
MimeType=application/x-ms-dos-executable;application/x-msi;
NoDisplay=false
Categories=Utility;
Icon=wine
```

Refresh Desktop database

```
update-desktop-database ~/.local/share/applications/
```

Now:

- Right-click your .exe file
- Choose Open With → Run Windows App with UMU
