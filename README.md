# NEEO Channel Editor (Web)

A free tool for editing your NEEO Brain's channel favorites - logos,
names, channel numbers, the "custom" flag, order, and more. Runs
entirely in your browser, right here:

## 👉 [https://ichrui.github.io/neeo-channel-editor/](https://ichrui.github.io/neeo-channel-editor/)

No install, no account, no download - just open the link above on a
device that's on the same local network as your NEEO Brain and go.


## What it does

- Loads your NEEO Brain's full channel/favorites list by IP address
- Edit channel name, logo URL, channel number, and the "custom" flag
- Add new channels, delete channels
- Reorder channels via drag & drop or up/down buttons - within a device,
  or copy a channel from one device to another
- **Find a logo automatically** based on the channel name (via Wikipedia),
  normalized to a square transparent PNG
- Group/collapse by room and device, search/filter
- Every change is written straight to your Brain the moment you save -
  no export/import step

There is no backend anywhere in this project. The page's JavaScript talks
**directly** to your NEEO Brain over your local network
(`http://<Brain-IP>:3000/...`). Nothing about your setup - not your
Brain's IP, not your channel list, nothing - is ever sent anywhere else,
including to whoever hosts this page.


## Usage

1. Open **[the link above](https://ichrui.github.io/neeo-channel-editor/)**
   on a device that's on the **same local network** as your NEEO Brain
   (see [Browser compatibility](#browser-compatibility) below - this
   matters more than usual for this tool).
2. Enter your Brain's IP address (e.g. `192.168.1.135`) and click
   **"Load from Brain"**.
3. Edit away. Each row has its own **Save** button, or use **"Save all
   changes"** to save everything you've touched at once.


## Browser compatibility

**This is the part that trips people up, so please read it before
reporting a bug.**

This tool needs to make a request from this page (served over `https://`
by GitHub Pages) directly to your Brain (which only speaks plain
`http://`). Browsers call this **"mixed content"**, and different
browsers handle it very differently:

| Platform | Browser | Works? |
|---|---|---|
| macOS | **Brave** | ✅ Confirmed working |
| macOS | Chrome, Edge (Chromium-based) | ⚠️ Likely works (same engine as Brave), not explicitly tested |
| macOS / Windows | Firefox | ❓ Untested - Firefox's mixed-content handling is stricter than Chromium's in some cases, may or may not work |
| macOS | Safari | ❓ Untested on desktop, but see iOS note below - likely blocked |
| **iPhone / iPad (any browser)** | Safari, Chrome, Firefox, Edge, etc. | ❌ **Does not work** |

### Why it doesn't work on mobile

Every browser on iOS/iPadOS - regardless of its name or icon - is
required by Apple to use Safari's underlying engine (WebKit). WebKit
enforces mixed-content blocking strictly: it refuses outright to let an
`https://` page fetch from an `http://` address, with no way to override
this from a website (no button, no setting, no browser extension can fix
it - it's enforced at the OS level). Chromium-based browsers (Chrome,
Brave, Edge) currently only log a console warning for this specific
case and let the request through, which is why it works on those but not
on Safari/iOS.

### If a request/change appears to silently fail

Check your browser's developer console (`Cmd+Option+I` / `F12`) for an
error mentioning "Mixed Content" or "CORS" - that confirms it's this
issue, not a bug in the tool itself, and switching to a Chromium-based
browser (Brave, Chrome, Edge) should fix it.


## A note on the write API

Saving changes uses an endpoint
(`POST /v1/projects/home/rooms/<RoomKey>/devices/<DeviceKey>/favorites/<Index>`)
that isn't officially documented by NEEO - it's been gathered from the
NEEO community. It works reliably on the Brains it's been tested against,
but isn't guaranteed. If you're trying this for the first time, test
with one unimportant channel before editing a lot at once.


## Privacy

This tool sends data to exactly one place: your Brain's IP address, on
your own local network. It doesn't use cookies, analytics, or any
third-party service, except for one thing: the "Find logo" feature
queries Wikipedia's public API (`en.wikipedia.org`) with the channel
name you're searching for, to find a matching logo image. No other data
leaves your network at any point.
