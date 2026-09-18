# MusicBrainz Integration

MusicBrainz is a free, open-source music encyclopedia. Discography can search it to discover releases, view rich metadata, and import albums directly into your collection.

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

You can also enrich an album already in your collection: open its detail view, tap the **MusicBrainz toolbar button**, and the app will look up the album's MusicBrainz ID (if stored) and fill in any fields that are currently empty — tracks, credits, cover art URL.

---

## Barcode Scanner

On iOS, tap the **barcode icon** in the toolbar (or Scan Barcode on the Home screen). The camera opens and scans for a UPC or EAN barcode printed on the album packaging.

When a barcode is recognized:

1. The scanner closes automatically.
2. The app switches to MusicBrainz mode.
3. A search for `barcode:<scanned-value>` is submitted.
4. Matching releases appear in the list.

From there, tap a result and tap **Add to Collection** to import it.
