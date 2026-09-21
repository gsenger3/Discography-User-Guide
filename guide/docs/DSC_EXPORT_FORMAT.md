# Discography Export Format (.dsc)

This document describes the `.dsc` archive format produced by the **Export Discography to JSON** feature.

---

## Archive Overview

A `.dsc` file is a standard ZIP archive with a renamed extension. It can be opened with any ZIP utility (macOS Archive Utility, 7-Zip, unzip, etc.) by renaming the extension to `.zip`, or by passing it directly to a ZIP-aware tool.

### Filename

Archives are named using a compact ISO timestamp:

```
Discography-<yyyyMMdd-HHmmss>.dsc
```

Example: `Discography-20260906-143022.dsc`

### Save Location

The destination folder is chosen by the user in the Export window before starting the export. The folder picker defaults to:

```
~/Documents/Discography/
```

Any folder on the local file system can be selected. The chosen folder is created automatically if it does not already exist. The export window's progress log confirms the exact destination path before the archive is created.

---

## Archive Structure

```
Discography-20260906-143022.dsc
├── discography.json       ← complete album database
└── img/
    ├── Abbey Road.jpg
    ├── Kind of Blue.jpg
    └── ...                ← one file per album with cover art
```

### `discography.json`

The primary data file. UTF-8 encoded, pretty-printed JSON. See the schema below.

### `img/`

Contains cover art for albums that have artwork stored in the database. Each file is named after the album title with path-unsafe characters (`/ \ : * ? " < > |`) replaced by underscores. The image data is written as-is from the database (typically JPEG); the `.jpg` extension is used regardless of source format.

Albums with no stored cover art are omitted from this folder. Their `coverArtFile` field in the JSON will be `null`.

---

## Schema Version History

| Version | What changed |
|---------|-------------|
| `"1.0"` | Initial release |
| `"1.1"` | Added `tags` field (`array<string>`) to Album objects |
| `"1.2"` | Added `side` field (`string \| null`) to Track objects to support multi-sided media (Vinyl, Cassette) |

Importers should treat unknown fields as optional and fall back gracefully on older versions.

---

## JSON Schema

### Top-level document

```json
{
  "exportDate": "2026-09-06T14:30:22Z",
  "version": "1.2",
  "albumCount": 142,
  "albums": [ ... ]
}
```

| Field | Type | Description |
|-------|------|-------------|
| `exportDate` | `string` (ISO 8601) | UTC timestamp of when the export was created |
| `version` | `string` | Schema version. Currently `"1.2"` |
| `albumCount` | `integer` | Number of album objects in `albums` |
| `albums` | `array<Album>` | Complete list of album records |

---

### Album object

```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "title": "Abbey Road",
  "artist": "The Beatles",
  "year": 1969,
  "country": "GB",
  "musicBrainzID": "b84ee12a-09ef-421b-82de-0441a926375b",
  "format": "Vinyl",
  "releaseType": "Album",
  "upc": "094638246824",
  "catalogNumber": "PCS 7088",
  "coverArtFile": "img/Abbey Road.jpg",
  "label": "Apple Records",
  "rating": 5,
  "mediaCondition": "NM",
  "sleeveCondition": "VG+",
  "notes": "Original UK pressing.",
  "reissueYear": null,
  "matrixNotes": "YEX 749-1 / YEX 750-1",
  "tags": ["Rock", "Progressive Rock", "Import"],
  "tracks": [ ... ],
  "credits": [ ... ]
}
```

| Field | Type | Nullable | Description |
|-------|------|----------|-------------|
| `id` | `string` (UUID) | No | Stable internal identifier |
| `title` | `string` | No | Album title |
| `artist` | `string` | No | Primary artist or band name |
| `year` | `integer` | No | Original release year (`0` if unknown) |
| `country` | `string` | Yes | Two-letter ISO 3166-1 alpha-2 country code, or `"XW"` (worldwide) / `"XE"` (Europe) |
| `musicBrainzID` | `string` (UUID) | Yes | MusicBrainz Release ID |
| `format` | `string` | No | Physical media format. See [Format values](#format-values) |
| `releaseType` | `string` | Yes | Release category. See [Release type values](#release-type-values) |
| `upc` | `string` | Yes | Universal Product Code (barcode) |
| `catalogNumber` | `string` | Yes | Label catalog number |
| `coverArtFile` | `string` | Yes | Relative path to the image within the archive (e.g. `"img/Abbey Road.jpg"`). `null` if no artwork |
| `label` | `string` | Yes | Record label name |
| `rating` | `integer` (0–5) | No | User rating. `0` = unrated |
| `mediaCondition` | `string` | Yes | Physical condition of the media. See [Condition values](#condition-values) |
| `sleeveCondition` | `string` | Yes | Physical condition of the sleeve/cover. See [Condition values](#condition-values) |
| `notes` | `string` | Yes | Free-text user notes |
| `reissueYear` | `integer` | Yes | Year of the specific pressing/reissue, if different from `year` |
| `matrixNotes` | `string` | Yes | Vinyl matrix / runout groove inscription |
| `tags` | `array<string>` | No | User-defined ad-hoc categorization tags (empty array if none) |
| `tracks` | `array<Track>` | No | Ordered list of tracks (empty array if none recorded) |
| `credits` | `array<Credit>` | No | List of personnel credits (empty array if none recorded) |

---

### Track object

```json
{
  "position": 1,
  "discNumber": 1,
  "side": "A",
  "title": "Come Together",
  "durationMS": 259000
}
```

| Field | Type | Nullable | Description |
|-------|------|----------|-------------|
| `position` | `integer` | No | Track number within the disc/side group (1-based). Resets to 1 at the start of each new side (for multi-sided formats) or each disc |
| `discNumber` | `integer` | No | Disc number for multi-disc releases (1-based). Always `1` for single-disc releases |
| `side` | `string` | Yes | Physical side label for multi-sided formats (e.g. `"A"`, `"B"` for Vinyl; `"A"`, `"B"` for Cassette). `null` for formats without physical sides (CD, DVD, etc.) |
| `title` | `string` | No | Track title |
| `durationMS` | `integer` | Yes | Duration in milliseconds. `null` if unknown |

Tracks are sorted in the JSON by `discNumber` ascending, then `side` ascending (alphabetical, `null` values first), then `position` ascending.

#### Multi-sided media notes

For **Vinyl** and **Cassette** releases, `side` carries the physical side label entered by the user (typically `"A"` and `"B"`, but custom values are allowed). `position` is 1-based within each `(discNumber, side)` group — it resets to 1 at the start of each side.

For all other formats (CD, DVD, Blu-Ray, 8-Track, Other), `side` is `null` and `position` is 1-based within each `discNumber`.

---

### Credit object

```json
{
  "role": "Producer",
  "name": "George Martin"
}
```

| Field | Type | Nullable | Description |
|-------|------|----------|-------------|
| `role` | `string` | No | Production role (e.g. `"Producer"`, `"Engineer"`, `"Mastering"`) |
| `name` | `string` | No | Person or entity name |

---

## Enumeration Values

### Format values

Stored in the `format` field.

| Value | Description | Multi-sided |
|-------|-------------|-------------|
| `"Vinyl"` | Vinyl record (LP, 7", 10", 12") | Yes — sides labeled per disc |
| `"CD"` | Compact disc | No |
| `"Cassette"` | Cassette tape | Yes — sides labeled per tape |
| `"DVD"` | DVD video or audio | No |
| `"Blu-Ray"` | Blu-ray disc | No |
| `"8-Track"` | 8-track cartridge | No |
| `"Other"` | Any other physical format | No |

### Release type values

Stored in the `releaseType` field.

| Value | Description |
|-------|-------------|
| `"Album"` | Full-length album or LP |
| `"EP"` | Extended play |
| `"Single"` | Single |
| `"Comp"` | Compilation |

### Condition values

Used by both `mediaCondition` and `sleeveCondition`.

| Value | Full name |
|-------|-----------|
| `"M"` | Mint |
| `"NM"` | Near Mint |
| `"VG+"` | Very Good Plus |
| `"VG"` | Very Good |
| `"G+"` | Good Plus |
| `"G"` | Good |
| `"F"` | Fair |
| `"P"` | Poor |

---

## Complete Example

The following example shows a Vinyl album with two sides, demonstrating multi-disc/multi-sided track layout.

```json
{
  "albumCount": 1,
  "albums": [
    {
      "artist": "The Beatles",
      "catalogNumber": "PCS 7088",
      "country": "GB",
      "coverArtFile": "img/Abbey Road.jpg",
      "credits": [
        {
          "name": "George Martin",
          "role": "Producer"
        }
      ],
      "format": "Vinyl",
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "label": "Apple Records",
      "matrixNotes": "YEX 749-1 / YEX 750-1",
      "mediaCondition": "NM",
      "musicBrainzID": "b84ee12a-09ef-421b-82de-0441a926375b",
      "notes": "Original UK pressing.",
      "rating": 5,
      "reissueYear": null,
      "releaseType": "Album",
      "sleeveCondition": "VG+",
      "tags": ["Rock", "Classic"],
      "title": "Abbey Road",
      "tracks": [
        {
          "discNumber": 1,
          "durationMS": 259000,
          "position": 1,
          "side": "A",
          "title": "Come Together"
        },
        {
          "discNumber": 1,
          "durationMS": 187000,
          "position": 2,
          "side": "A",
          "title": "Something"
        },
        {
          "discNumber": 1,
          "durationMS": 242000,
          "position": 1,
          "side": "B",
          "title": "Here Comes the Sun"
        },
        {
          "discNumber": 1,
          "durationMS": 462000,
          "position": 2,
          "side": "B",
          "title": "The End"
        }
      ],
      "upc": null,
      "year": 1969
    }
  ],
  "exportDate": "2026-09-06T14:30:22Z",
  "version": "1.2"
}
```

> **Note:** The JSON encoder sorts keys alphabetically. Field order in the file will always be alphabetical within each object.

---

## Opening a .dsc Archive

### macOS
Double-click the file in Finder — macOS Archive Utility will expand it automatically, or rename to `.zip` first if needed.

### Command line
```sh
unzip Discography-20260906-143022.dsc -d Discography-Export/
```
