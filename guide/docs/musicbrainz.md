# MusicBrainz Integration

MusicBrainz is a free, open-source music encyclopedia. Discography can search it to discover releases, view rich metadata, and import albums directly into your collection or Wishlist.

---

## MusicBrainz Search

### Switching to MusicBrainz Mode

Tap the **MusicBrainz icon** in the toolbar. The icon gets a highlighted border and the sidebar list switches to MusicBrainz results. The search prompt changes to "Search MusicBrainz…".

### Running a Search

Type your query in the search field and press **Return / Enter**. Results load from the MusicBrainz API and appear in the list. Each result shows cover art (if available), title, artist, year, country flag, and format badge.

Simple MusicBrainz search accepts any combination of:

- Artist name
- Album / release title
- Barcode (UPC/EAN)
- Catalog number

Results are paginated. Scroll to the bottom of the list to automatically load the next page.

The format filter and sort controls at the top of the sidebar apply to MusicBrainz results the same way they do to your local collection.

> Note: Sometimes MusicBrainz fails to or returns incomplete results. The recommended course of action is to refresh the search. Select the `Refresh` button on `macOS` or pull down to refresh on `iOS`. 

### Result Row Actions

**Right-click / long-press** any result row for a context menu with:

| Action | Description |
|---|---|
| Add to Collection | Imports the release into your collection immediately, without opening the detail view |
| Add to Wishlist | Adds the release to your Wishlist immediately, without opening the detail view |

### Exiting MusicBrainz Mode

Tap the MusicBrainz icon again, tap the Discography logo to go Home, or (on `iOS`) cancel the search to exit MusicBrainz mode.

---

## Advanced MusicBrainz Search

MusicBrainz supports a field-based query syntax. You can use it directly in the search field while in MusicBrainz mode.

### Supported Keys

| Key | Short forms | Searches |
|---|---|---|
| `artist` | `a=`, `a:` | Artist name |
| `album` | `release`, `title`, `r=`, `r:` | Release/album title |
| `label` | `l=`, `l:` | Record label |
| `barcode` | `upc`, `b=`, `b:` | UPC / EAN barcode |
| `catno` | `catalog`, `c=`, `c:` | Catalog number |
| `year` | `y=`, `y:` | Release year |
| `country` | (none) | Country code |

Both `=` and `:` can be used as separators between a key and its value.

### Examples

```
artist=Pink Floyd
artist=Pink Floyd album=Dark Side of the Moon
label=Harvest year=1973
barcode=724382975229
catno=SHVL 8047
a=Bowie r=Heroes
```

A hint card is shown in the MusicBrainz detail panel whenever the search field is empty — it lists all supported keys and example queries for quick reference.

When an advanced MusicBrainz query is active, an <span style="background-color: #efc977; color: #1e293b; padding: 4px 12px; border-radius: 9999px; font-size: 0.85em; font-weight: 500;">Advanced</span> badge appears in the results banner.

---

## Importing from MusicBrainz

1. Switch to MusicBrainz mode and search for the release you want.
2. Tap a result row to open its detail view.
3. The detail view shows full metadata: release info, complete tracklist (loaded from MusicBrainz), credits, and cover art.
4. Tap **Add to Collection** in the toolbar.

The album is added to your collection with:
- Title, artist, year, country, label, UPC, catalog number, release type, and MusicBrainz ID
- Full tracklist with positions, disc numbers, and durations
- Credits (producers, engineers, etc.)
- Cover art downloaded and stored locally for offline access

After import the button changes to **Added to Collection** (green checkmark) and becomes disabled.

---

## Adding to Your Wishlist from MusicBrainz

From a MusicBrainz release detail view, tap the **heart (Add to Wishlist)** button in the toolbar to save the release to your Wishlist without adding it to your collection. The item is saved with full metadata and cover art.

After tapping, the button changes to **Added to Wishlist** (filled heart) and becomes disabled.

You can also right-click / long-press any result row in the MusicBrainz list and choose **Add to Wishlist** to add it directly without opening the detail view.

For details on managing your Wishlist, see the [Wishlist](wishlist.md) page.

---

## Metadata Enrichment

Discography can enrich albums already in your collection with metadata from MusicBrainz — tracklists, credits, cover art, label, catalog number, country, and more. Enrichment runs in the background one album at a time, respecting MusicBrainz API rate limits.

### The MusicBrainz Toolbar Button (Album Detail)

When viewing an album in your collection, the **MusicBrainz icon** appears in the toolbar. Tapping it opens a menu with two enrichment actions:

| Option | What it does |
|---|---|
| **Match Album** | Searches MusicBrainz and fills in any empty fields. Existing data is not overwritten. |
| **Fix Match** | Opens a list of all matching releases so you can pick the exact pressing. Replaces all metadata with your selection. |

When enrichment is actively running, the toolbar icon changes to a **spinner**. Tapping the spinner opens a progress dialog showing which album is currently being processed, with a **Cancel Enrichment** option to stop the queue.

### Match Album

**Match Album** uses the most specific identifier available to find the right release:

1. **Barcode (UPC)** — most precise; used if present
2. **Catalog number + artist** — used if a catalog number is stored  
3. **Artist, title, year, country** — broad text match as a fallback

Only **empty** fields are updated. Any data already on the album is left unchanged, making Match Album safe to run on partially-filled entries.

When the match completes, a timestamped status note is appended to the album's **Notes** field listing which fields were updated.

> Note: MusicBrainz can be quite strict when performing barcode and catalog matches, if your album is not found, verify these fields are correct. Alternatively, use the fix match feature to perform a looser search and choose from a wider range of releases.

### Fix Match

Use **Fix Match** when the automatic match selected the wrong pressing, region, or edition of a release.

Fix Match opens a sheet showing all MusicBrainz releases for the album's artist and title. Each row shows cover art, title, artist, label, catalog number, country, year, and format. Tap any row to apply it.

**Fix Match replaces all metadata**, including:

- Artist, title, year, country
- Format and release type
- Label and catalog number
- Barcode
- Cover art
- Full tracklist
- Credits

A timestamped note is appended to the **Notes** field recording the manual match and which fields changed.

### Auto-Enrich on First Save

When you add a new album and save it for the first time, Discography automatically queues it for MusicBrainz enrichment. No manual action is required — metadata fills in shortly after saving.

### Discogs Import Auto-Enrichment

After importing a collection from a Discogs CSV export, all imported albums are automatically queued for MusicBrainz enrichment. See [Discogs Import](DISCOGS_IMPORT_FORMAT.md) for details on the import process.

### Enrichment Notes Log

Every enrichment action appends a status entry to the album's **Notes** field. Examples:

```
MusicBrainz: Matched on 10/9/26. Updated: Year, Country, Cover Art, Tracklist (12 tracks).
MusicBrainz: Manual match on 10/9/26. Updated: Artist, Title, Format, Label, Tracklist (10 tracks).
MusicBrainz: No match found (10/9/26).
```

This provides an audit trail of when an album was enriched and what changed.

---

## Barcode Scanner

On iOS, tap the **barcode icon** in the toolbar (or Scan Barcode on the Home screen). The camera opens and scans for a UPC or EAN barcode printed on the album packaging.

When a barcode is recognized:

1. The scanner closes automatically.
2. The app switches to MusicBrainz mode.
3. A search for `barcode:<scanned-value>` is submitted.
4. Matching releases appear in the list.

From there, tap a result and tap **Add to Collection** to import it, or **Add to Wishlist** to save it for later.
