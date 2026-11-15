# Server version (Raspberry Pi / Mac)

`neeo_channel_editor.py` is the self-hosted version of the editor (stdlib-only Python, serves the page on port 8642).
It is optimised for the iPhone and can update itself: the page shows the installed version and an
**Update now** button when a newer `APP_VERSION` is found in this folder.

Run: `python3 neeo_channel_editor.py`  
Updates: bump `APP_VERSION` in the script and push to `main`; press **Update now** in the page.

## Saving logos on the Brain
"Save to Brain" in the logo search copies the 256x256 PNG into the Brain's logo folder
(`/opt/mobile/eui/pics`, served at `http://<brain>:3200/eui/pics/`) over SSH with a key file
(default `~/.ssh/neeoblackbrainkey.id_rsa`, user `neeo`; override with `NEEO_BRAIN_KEY`, `NEEO_BRAIN_USER`)
and fills in the logo link. File name = channel name, lowercase, no spaces (editable).

## Settings (gear, top right)
- **Brain IP** is stored on the server (`~/.neeo-channel-editor/settings.json`), so every device uses the same address.
- **Backups**: before the first change after loading, the Brain's data is saved to `~/.neeo-channel-editor/backups/` (last 40 kept).
  "Create backup now" saves the current Brain state; "Restore" puts one device's channel list back
  (the current state is backed up first, then the page reloads from the Brain).
- **Software update** (see above).
