# Changelog

All notable changes to the NEEO Channel Editor (Web) are documented here.


## [Unreleased]

### Added
- Logo search now also uses the [tv-logo/tv-logos](https://github.com/tv-logo/tv-logos)
  collection on GitHub (~10,000 TV logos) as its first source, before
  Wikipedia. Matches follow the repository's naming scheme (e.g. "SRF 1"
  finds `srf-1-ch.png`, "ORF 1" finds `orf1-at.png`); Swiss, German and
  Austrian channels are ranked first. Each result shows its source.
- The file list of the repository is built into the page (no API calls,
  no rate limits).

### Fixed
- Removed a leftover analytics setup comment in the page `<head>` that
  had a bug causing part of its own instructional text to render as
  visible text at the top of the page, instead of staying hidden as
  intended.


## v1.4

### Added
- Adding a channel that already exists (by name) on another device now
  auto-fills its logo, channel number, and "custom" flag, instead of
  requiring you to look them up and re-enter them. Fields you've
  already filled in yourself are left untouched; if your entry
  conflicts with the existing one, you get a one-click "use that
  instead" suggestion rather than a silent overwrite.

### Removed
- "All visible → Custom OFF/ON" and "Download edited file" toolbar
  buttons (unused in the live-Brain workflow this tool is built around).


## v1.3

### Added
- **Find logo**: search for a channel's logo automatically by name, via
  Wikipedia's public API. Results are normalized to square, transparent
  256×256 PNGs regardless of the original image's shape or format, so
  every logo looks consistent. Each result can be used directly (as an
  external link) or downloaded as a PNG file.

### Fixed
- Device/room group order could shift unexpectedly after reordering
  channels within a group (moving or dragging channels no longer moves
  the whole device to a different position in the list - group order is
  now taken from a fixed list captured when the data was loaded, not
  from wherever channels currently sit in memory).
- Dragging a channel into a *different* device group always appended it
  to the end of that group, ignoring the exact spot it was dropped on;
  it's now inserted exactly where you drop it.
- Inconsistent vertical spacing between device group headers, caused by
  a CSS quirk (`position: sticky` on multiple stacked table headers
  renders inconsistently across browsers) - group headers now use
  normal positioning instead.


## v1.2

### Removed
- The manual "Load backup file" option and the automatic backup
  download that used to trigger on every load from a Brain. The tool
  now assumes a live Brain connection throughout; use your browser's
  own history/bookmark if you want to keep a record of a session.


## v1.1

### Changed
- Rebuilt as a fully static, serverless page: every request (load, save,
  add, delete, reorder) goes directly from the browser to the Brain over
  your local network via its REST API. No backend, no server, no
  installation - confirmed the Brain allows direct cross-origin browser
  requests for both reading and writing.


## v1.0 - Initial release

### Added
- Load a NEEO Brain's full channel/favorites list by IP address
- Edit channel name, logo URL, channel number, and the "custom" flag
- Add and delete channels
- Reorder channels via drag & drop or up/down buttons, within a device
  or copied across devices
- Group by room/device with collapsible headers, search/filter, bulk
  custom-flag toggles
- Save individual changes or all changes at once
