# build-fittsmon-gui-appimage

Builds a self-contained [AppImage](https://appimage.org/) for [fittsmon-gui](https://github.com/musqz/fittsmon-gui) — the GTK3 configuration GUI for the [fittsmon](https://github.com/musqz/fittsmon) daemon.

---

## Requirements

| Tool | Purpose |
|------|---------|
| `git` | Clone / update the fittsmon-gui repo |
| `appimagetool` | Package the AppImage |
| `magick` (ImageMagick) | Rasterize the SVG icon to PNG |
| `python3` + `python3-gi` | Runtime dependency check |

**Install on Arch / Mabox:**
```bash
sudo pacman -S imagemagick python-gobject 
yay -S appimagetool-bin
```
Or Download `appimagetool` from [github.com/AppImage/appimagetool/releases](https://github.com/AppImage/appimagetool/releases) and place it somewhere in your `$PATH`.

---

## Usage

```bash
git clone https://github.com/musqz/build-fittsmon-gui-appimage.git
cd build-fittsmon-gui-appimage
chmod +x build-fittsmon-gui-appimage
./build-fittsmon-gui-appimage
```

The AppImage is created at:
```
fittsmon-gui-build/FittsmonGui-<version>-x86_64.AppImage
```

On subsequent runs the script updates the cloned repo automatically — no need to re-clone.

---

## What it does

1. Clones (or updates) the fittsmon-gui repository
2. Creates an AppDir with the Python script, icon, man page, desktop file, and AppStream metadata
3. Rasterizes the SVG icon to PNG for appimagetool
4. Verifies GTK3 + python3-gi are available on the build host
5. Packages everything into a single portable AppImage

---

## Notes

- The AppImage relies on **system Python 3 and GTK3** — it does not bundle a Python runtime
- Requires the `fittsmon` daemon to be installed separately: [github.com/musqz/fittsmon](https://github.com/musqz/fittsmon)
- Version is read from `git describe --tags` on the fittsmon-gui repo
