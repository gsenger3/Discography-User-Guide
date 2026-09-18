# Discogs CSV Import Format

This document describes the CSV file format accepted by the **Import Discogs CSV** feature, which imports a Discogs collection export into Discography.

---

## Obtaining the CSV from Discogs

1. Log in at [discogs.com](https://www.discogs.com)
2. Go to **My Collection** → **Export Collection**
3. Download the generated `.csv` file
4. In Discography, choose **File → Import Discogs CSV...** and select the file

---

## File Requirements

| Property | Requirement |
|----------|-------------|
| Encoding | UTF-8 |
| Line endings | `\n`, `\r\n`, or `\r` (all normalised on import) |
| Delimiter | Comma (`,`) |
| Quoting | Fields may be wrapped in double quotes; internal double quotes are escaped as `""` |
| Header row | **Required** — first row must contain column names |

---

## Columns

### Required columns

These columns must be present or the import will be rejected with an error.

| Column name | Maps to | Notes |
|-------------|---------|-------|
| `Title` | `Album.title` | Album title |
| `Artist` | `Album.artist` | Artist or band name |

### Optional columns

All other columns are imported when present; missing or blank values are silently ignored.

| Column name | Maps to | Notes |
|-------------|---------|-------|
| `Released` | `Album.year` | Integer year. Non-numeric values default to `0` |
| `Catalog#` | `Album.catalogNumber` | Label catalog number |
| `Label` | `Album.label` | Record label name |
| `Rating` | `Album.rating` | Integer 1–5. Non-numeric or blank values default to `0` |
| `Format` | `Album.format` + `Album.releaseType` | Comma-separated; first part maps to media format, second part (if present) maps to release type. See [Format parsing](#format-parsing) |
| `Media Condition` | `Album.mediaCondition` | Preferred column name for media condition |
| `Collection Media Condition` | `Album.mediaCondition` | Alternate column name used by some Discogs export versions; used if `Media Condition` is absent |
| `Collection Sleeve Condition` | `Album.sleeveCondition` | Sleeve/cover condition |
| `Collection Notes` | `Album.notes` | Free-text collection notes |

> **Note:** Columns not listed above but are present in Discogs exports are not currently imported (e.g. `Discogs ID`, `Discogs Seller`, `Ships From`, `Price`). They are ignored without error.

---

## Format Parsing

The `Format` column in a Discogs export contains a comma-separated string combining media type and release category, for example:

```
Vinyl, Album, LP
CD, Album
Vinyl, EP, 7"
```

The importer reads only the **first two** comma-separated parts:

- **Part 1** → media format (see [Format mapping](#format-mapping))
- **Part 2** → release type (see [Release type mapping](#release-type-mapping)); omitted parts leave `releaseType` unset

---

## Value Mappings

### Format mapping

The first part of the `Format` field is matched case-insensitively.

| Input value(s) | Stored as |
|----------------|-----------|
| `vinyl`, any value containing `lp`, `7"`, `10"`, or `12"` | `Vinyl` |
| `cd`, any value containing `cd` | `CD` |
| `cassette` | `Cassette` |
| `dvd` | `DVD` |
| `blu-ray` | `Blu-Ray` |
| `8-track cartridge`, `8-track` | `8-Track` |
| Anything else | `Other` |

### Release type mapping

The second comma-separated part of the `Format` field is matched case-insensitively.

| Input value(s) | Stored as |
|----------------|-----------|
| `album`, `lp` | `Album` |
| `ep` | `EP` |
| `single` | `Single` |
| `compilation`, `comp` | `Comp` |
| Anything else | *(not set)* |

### Condition mapping

Applied to both `Media Condition` / `Collection Media Condition` and `Collection Sleeve Condition`.

The importer accepts both the abbreviated form used by Discography and the full verbose form used by Discogs exports.

| Discogs verbose form | Abbreviated form | Stored as |
|----------------------|-----------------|-----------|
| `Mint (M)` | `M` | `M` |
| `Near Mint (NM or M-)` | `NM` | `NM` |
| `Very Good Plus (VG+)` | `VG+` | `VG+` |
| `Very Good (VG)` | `VG` | `VG` |
| `Good Plus (G+)` | `G+` | `G+` |
| `Good (G)` | `G` | `G` |
| `Fair (F)` | `F` | `F` |
| `Poor (P)` | `P` | `P` |
| *(blank or unrecognised)* | — | *(not set)* |

Matching is done by prefix, so partial strings like `"Near Mint"` and `"Very Good Plus (VG+)"` are both recognised.

---

## What Is Not Imported

The following data is **not** present in a Discogs CSV and will not be populated on import:

- Cover art (artwork must be added manually or via MusicBrainz lookup)
- Track listing
- Personnel credits
- MusicBrainz ID
- UPC / barcode
- Country
- Reissue year
- Matrix / runout notes

---

## Example CSV

```csv
Catalog#,Artist,Title,Label,Format,Rating,Released,Collection Media Condition,Collection Sleeve Condition,Collection Notes
PCS 7088,The Beatles,Abbey Road,Apple Records,"Vinyl, Album, LP",5,1969,Very Good Plus (VG+),Very Good (VG),Original UK pressing.
CK 40579,Miles Davis,Kind of Blue,Columbia,"CD, Album",5,1959,Near Mint (NM or M-),Near Mint (NM or M-),
,The Velvet Underground,The Velvet Underground & Nico,Verve,"Vinyl, Album",4,1967,Very Good (VG),Good Plus (G+),Banana cover.
```

> **Tip:** Column order does not matter — the importer maps columns by name, not position.
