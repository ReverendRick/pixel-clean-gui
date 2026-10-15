# PG32UCDM Pixel Clean

GTK4 GUI for triggering the ASUS ROG Swift OLED PG32UCDM built-in pixel cleaning routine via DDC/CI.

## Requirements

- `ddcutil`
- GTK4 + libadwaita + python-gobject
- Python 3.14+

## Install

```bash
# 1. Clone the repo
git clone https://github.com/ReverendRick/pixel-clean-gui.git
cd pixel-clean-gui

# 2. Install dependencies
sudo pacman -S ddcutil gtk4 libadwaita python-gobject

# 3. Install application files
install -Dm755 pixel-clean-gui      ~/.local/bin/pixel-clean-gui
install -Dm755 pixel-clean-gui-launcher ~/.local/bin/pixel-clean-gui-launcher
install -Dm644 pixel-clean-gui.desktop /usr/share/applications/pixel-clean-gui.desktop

# 4. Refresh desktop database (KDE/GNOME)
kbuildsycoca6 --noincremental 2>/dev/null || true
update-desktop-database ~/.local/share/applications 2>/dev/null || true
```

## CLI

```bash
pixel-clean-gui
```

## Desktop Entry

`pixel-clean-gui.desktop` is installed to `/usr/share/applications/`.

## How it works

Reads VCP code `0xFD`, computes `current + 16` (max `30841` / `0x7879`), writes it with `ddcutil setvcp --noverify`, then restores the original value after the ~6 minute cleaning cycle.

## Files

- `pixel-clean-gui` — GTK4/Adwaita application
- `pixel-clean-gui-launcher` — sets `PYTHONPATH` for the bundled Python environment
- `pixel-clean-gui.desktop` — XDG desktop entry
