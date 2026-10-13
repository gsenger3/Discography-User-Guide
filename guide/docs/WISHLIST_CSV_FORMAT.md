# Wishlist CSV Format

This document describes the CSV file format produced by **Export Wishlist CSV** and accepted by **Import Wishlist CSV** (`macOS`).

---

## File Overview

A Wishlist CSV export is a plain UTF-8 text file containing one wishlist item per row. It can be opened in any spreadsheet application (Numbers, Excel, Google Sheets) and re-imported into Discography.

### Filename

Export files are named using a compact ISO timestamp:

```
Wishlist-<yyyyMMdd-HHmmss>.csv
```

Example: `Wishlist-20261012-143022.csv`

### Save Location

The destination folder is chosen by the user in the Export window. The folder picker defaults to:

```
~/Documents/Discography/
```

Any folder on the local file system can be selected. The chosen folder is created automatically if it does not already exist.

---

## File Requirements

| Property | Requirement |
|----------|-------------|
| Encoding | UTF-8 |
| Line endings | `\n` (LF) on export; `\n`, `\r\n`, or `\r` all accepted on import |
| Delimiter | Comma (`,`) |
| Quoting | All fields are wrapped in double quotes on export; internal double quotes are escaped as `""` (RFC 4180) |
| Header row | **Required** — first row must contain column names |

---

## Columns

Column order does not matter — the importer maps columns by name, not by position.

### Required columns (import)

These columns must be present or the import will fail with an error.

| Column | Type | Notes |
|--------|------|-------|
| `title` | string | Wishlist item title |
| `artist` | string | Artist or band name |

### All columns

| Column | Type | Nullable | Notes |
|--------|------|----------|-------|
| `title` | string | No | Item title |
| `artist` | string | No | Artist or band name |
| `year` | integer | No | Release year. `0` = unknown |
| `country` | string | Yes | Two-letter ISO 3166-1 alpha-2 country code (e.g. `US`, `GB`), `XW` (worldwide), or `XE` (Europe). Blank = unknown |
| `musicBrainzID` | string (UUID) | Yes | MusicBrainz Release ID |
| `format` | string | Yes | Physical media format. See [Format values](#format-values). Blank or unrecognised values default to `CD` |
| `releaseType` | string | Yes | Release category. See [Release type values](#release-type-values). Blank = none set |
| `upc` | string | Yes | Universal Product Code (barcode) |
| `catalogNumber` | string | Yes | Label catalog number |
| `label` | string | Yes | Record label name |
| `notes` | string | Yes | Free-text personal notes (may contain newlines) |
| `dateAdded` | string (ISO 8601 UTC) | Yes | Timestamp when the item was added to the Wishlist. Blank values default to the current time on import |

> **Note:** Cover art is not included in the CSV export. Artwork must be re-added manually or via MusicBrainz lookup after importing.

---

## Import Modes

The import panel offers two modes:

| Mode | Behaviour |
|------|-----------|
| **Replace Wishlist** | All existing wishlist items are deleted before the new items are inserted |
| **Append to Wishlist** | New items are added alongside existing items. No duplicate detection is performed |

---

## Enumeration Values

### Format values

Stored in the `format` column. Values are case-sensitive on export; recognised case-insensitively on import.

| Value | Description |
|-------|-------------|
| `Vinyl` | Vinyl record (LP, 7", 10", 12") |
| `CD` | Compact disc |
| `Cassette` | Cassette tape |
| `DVD` | DVD video or audio |
| `Blu-Ray` | Blu-ray disc |
| `8-Track` | 8-track cartridge |
| `Other` | Any other physical format |

### Release type values

Stored in the `releaseType` column.

| Value | Description |
|-------|-------------|
| `Album` | Full-length album or LP |
| `EP` | Extended play |
| `Single` | Single |
| `Comp` | Compilation |

---

## What Is Not Included

The following data is not exported to CSV:

- Cover art (embedded image data)
- Tracklist
- Credits
- Tags

These fields become available after moving a wishlist item into your collection.

---

## Example

```csv
"title","artist","year","country","musicBrainzID","format","releaseType","upc","catalogNumber","label","notes","dateAdded"
"Abbey Road","The Beatles","1969","GB","b84ee12a-09ef-421b-82de-0441a926375b","Vinyl","Album","094638246824","PCS 7088","Apple Records","Original UK pressing.","2026-10-05T10:30:00Z"
"Kind of Blue","Miles Davis","1959","US","","CD","Album","","CK 40579","Columbia","","2026-10-06T14:22:10Z"
"Never Mind the Bollocks","Sex Pistols","1977","GB","","Vinyl","Album","","V2086","Virgin Records","","2026-10-08T09:15:33Z"
```

> **Tip:** Column order does not matter — the importer maps columns by name. A CSV edited in a spreadsheet application and re-saved in a different column order will still import correctly.
