# Server version (Raspberry Pi / Mac)

`neeo_channel_editor.py` is the self-hosted version of the editor (stdlib-only Python, serves the page on port 8642).
It is optimised for the iPhone and can update itself: the page shows the installed version and an
**Update now** button when a newer `APP_VERSION` is found in this folder.

Run: `python3 neeo_channel_editor.py`  
Updates: bump `APP_VERSION` in the script and push to `main`; press **Update now** in the page.
