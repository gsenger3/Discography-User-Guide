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

Tags are free-form labels you can attach to any album for personal categorization — for example: `favorite`, `remaster`, `jazz`, `live`.

### Adding Tags in Edit Mode

1. Open an album and tap Edit.
2. Scroll to the **Tags** section.
3. Type a tag name in the text field. A dropdown appears with suggestions drawn from tags already used across your collection.
4. Press Return (_or select a suggestion with the arrow keys and press Return_) to add the tag.
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

Discography compiles your entire collection — album metadata, tracks, credits, tags, and embedded cover art — into a `.dsc` archive file.

1. Go to **File > Export…** to open the export panel.
1. Click **Choose Destination** to pick where the file is saved,
1. then click **Export**.

The export will run and a progress log updates in real time. You can cancel a long export at any time.

> Note: The `.dsc` archive file is a ZIP file containing a JSON database; it can be opened with any standard ZIP utility.

### Importing

Discography can import both `.dsc` archives and Discogs `.csv` export files.

1. Go to **File > Import…** to import a previously exported `.dsc` archive or a Discogs `.csv` export.
2. Click **Choose** to select the file you want to import.

> `.dsc` import will give you the option of appending the file to your collection or replacing it.

3. Click the **Import** button.
 
The import will begin. Discography `.dsc` imports will show a progress log and handles duplicates gracefully.

For details on the `.dsc` file format, see [DSC EXPORT FORMAT](DSC_EXPORT_FORMAT.md).
For the Discogs `.csv` format, see [DISCOGS IMPORT FORMAT](DISCOGS_IMPORT_FORMAT.md).
