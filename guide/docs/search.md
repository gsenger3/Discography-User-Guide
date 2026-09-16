# Searching Your Collection

This page covers simple and advanced search over your local collection.

---

## Simple Search

Type in the search field above the collection list to filter in real time. Simple search matches against:

- Album title
- Artist name
- UPC / barcode
- Catalog number
- Year
- Tags

The search is case-insensitive and matches partial strings. Clearing the search field restores the full list.

---

## Advanced Local Search

When your search text contains `=`, `~`, `<`, or `>` characters, Discography automatically switches to advanced search mode. An **Advanced** badge appears in the results banner.

Advanced search uses a structured `field=value` syntax to target specific fields and combine conditions with boolean logic.

### Field Names

| Field | Short forms | Matches |
|---|---|---|
| `title` | `album`, `release`, `r` | Album title |
| `artist` | `a` | Artist name |
| `year` | `y` | Original release year |
| `year2` | `y2` | Re-issue year |
| `country` | `cn` | Country code or name |
| `format` | `f` | Media format |
| `catalog` | `cat` | Catalog number |
| `releasetype` | `type` | Release type (Album, EP, Single, Comp) |
| `tag` | `t` | Any tag on the album |

### Match Operators

| Operator | Meaning |
|---|---|
| `=` | Exact (case-insensitive) |
| `~` | Contains (case-insensitive) |
| `<` | Less than (year fields only) |
| `<=` | Less than or equal (year fields only) |
| `>` | Greater than (year fields only) |
| `>=` | Greater than or equal (year fields only) |

### Boolean Operators

| Operator | Meaning |
|---|---|
| `&` | AND — both conditions must match |
| `\|` | OR — either condition must match |
| `!` | NOT — inverts the following condition |
| `( )` | Grouping — controls evaluation order |

### Multi-Value Shorthand

After the operator, separate multiple values with `:` (OR between values) or `,` (AND between values):

```
format=Vinyl:CD          matches Vinyl OR CD
tag=jazz,live            matches albums tagged both jazz AND live
```

### Examples

```
artist=Pink Floyd
a~floyd & year>1970
format=Vinyl & year>=1970 & year<=1979
artist=Bowie & !format=CD
(artist=Eno | artist=Fripp) & year<1980
tag=favourite
r~dark side
```

---

## Searching by Tag

In simple search, type any word that appears in a tag and matching albums are returned.

In advanced search use `tag=jazz` (exact) or `tag~jaz` (contains) to match tags specifically. Use `t=` as a shorthand.

To create, rename, or delete tags, see [Managing Tags](advanced.md#managing-tags).
