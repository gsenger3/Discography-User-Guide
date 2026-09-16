# Advanced Features

This page covers Settings, tag management, and importing/exporting your collection.

---

## Settings

Open Settings from the gear icon in the toolbar (iOS) or from the application menu / preferences (macOS).

| Setting | Description |
|---|---|
| Recently Added — Number of Albums to Display | Controls how many albums appear in the Home screen coverflow (1–99) |
| Tag Manager | Rename or delete tags across the entire collection |
| Version Info | Shows the current app version and build number |

---

## Managing Tags

Tags are free-form labels you can attach to any album for personal categorization — for example: `favourite`, `wants-remaster`, `jazz`, `live`.

### Adding Tags in Edit Mode

1. Open an album and tap Edit.
2. Scroll to the **Tags** section.
3. Type a tag name in the text field. A dropdown appears with suggestions drawn from tags already used across your collection.
4. Press Return (or select a suggestion with the arrow keys and press Return) to add the tag.
5. Tap the **×** on any pill to remove that tag.

### Managing Tags (Settings)

Open **Settings** and scroll to the **Tag Manager** section.

- All unique tags used in your collection are shown as pills.
- **Tap** a tag pill to rename it — the rename applies to every album that carries that tag.
- **Tap ×** on a pill to delete the tag — it is removed from all albums in the collection.

To search for albums by tag, see [Searching by Tag](search.md#searching-by-tag).

---

## Export and Import

### Exporting (macOS)

Go to **File > Export…** (or the Export menu item) to open the export panel. Discography compiles your entire collection — album metadata, tracks, credits, tags, and embedded cover art — into a `.dsc` archive file. The archive is a ZIP file containing a JSON database; it can be opened with any standard ZIP utility.

A progress log updates in real time. Click **Choose Destination** to pick where the file is saved, then click **Export**. You can cancel a long export at any time.

### Importing

Go to **File > Import…** to import a previously exported `.dsc` archive or a Discogs CSV export. The import view shows a progress log and handles duplicates gracefully.

For details on the `.dsc` file format, see `doc/DSC_EXPORT_FORMAT.md`.
For the Discogs CSV format, see `doc/DISCOGS_IMPORT_FORMAT.md`.
