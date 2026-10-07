# Wishlist

The Wishlist lets you track releases you want to acquire. Items live separately from your collection and can be moved into it with a single tap when you get the album.

---

## Accessing the Wishlist

Tap the **heart icon** in the toolbar to enter Wishlist mode. The sidebar switches from your collection to the Wishlist list and the heart icon becomes highlighted in pink. Tap it again, or tap the **Discography logo**, to return to your collection.

---

## Wishlist List

The Wishlist sidebar works similarly to the Collection list.

### Filtering and Sorting

A control strip above the list lets you:

- **Filter by format** — show only a specific media format or show all.
- **Sort** — by Artist, Album title, or Year.
- **Sort direction** — toggle ascending/descending order.

A total count banner shows how many items match the current filter and search.

### List Actions

- **Tap / click** an item to open its detail view.
- **Swipe left** `iOS` on a row to reveal a Delete button.
- **Right-click / long-press** a row for a context menu with:

| Action | Description |
|---|---|
| Add to Collection | Moves the item into your collection and removes it from the Wishlist |
| Duplicate | Creates a copy of the item in the Wishlist |
| Delete | Removes the item from the Wishlist |

### Toolbar Buttons

| Button | Action |
|---|---|
| Discography logo | Return to the collection Home screen |
| MusicBrainz icon | Switch to MusicBrainz search mode |
| Heart (highlighted) | Exit Wishlist mode |
| Trash | Delete the currently selected item |
| + | Add a new blank Wishlist item |

---

## Wishlist Item Detail

### Read-Only View

Tapping a Wishlist item opens its detail view. The layout mirrors the Album Detail view:

- A hero banner with blurred cover art, gradient, and a thumbnail on the right.
- Title and artist overlaid on the banner.
- **Format / Release Type** displayed below the banner.
- A pink **Wishlist** badge.
- Release metadata: year, country, label, UPC, and catalog number.
- **Added date** — shown centered below the divider, indicating when the item was added to your Wishlist.
- **Notes** — free-text notes (if set).

### Toolbar Buttons (read-only mode)

| Button | Action |
|---|---|
| Pencil / Edit | Switches to edit mode |
| Add to Collection | Moves the item into your collection and removes it from the Wishlist |

After tapping **Add to Collection**, the button changes to **Added to Collection** (green checkmark) and becomes disabled.

### Edit Mode

Tap **Edit** (pencil icon) to enter edit mode. Tap **Save** (checkmark) to commit, or **Cancel** (×) to discard.

#### Fields available in edit mode

| Field | Notes |
|---|---|
| **Album Title** | *Required* |
| **Artist** | *Required* |
| Year | Original release year |
| Country | Two-letter country code or full name |
| Format | Vinyl, CD, Cassette, DVD, Blu-Ray, 8-Track, Other |
| Release Type | Album, EP, Single, Compilation |
| Label | Record label |
| UPC / Barcode | Numeric barcode |
| Catalog Number | Label catalog number |
| MusicBrainz ID | UUID for the release on musicbrainz.org |
| Cover Art URL | Direct URL to cover art image |
| Notes | Free-text personal notes |

**Cover art** can be set by:

- Clicking the camera button on the artwork thumbnail to pick an image from your Photos library `iOS` or file system `macOS`.
- Dragging an image file onto the artwork thumbnail `macOS`.
- Right-clicking / long-pressing the thumbnail and choosing **Remove Artwork** to clear it.

> Note: Wishlist items do not support tracklists, credits, or tags. These fields are available when the item is moved into your collection.

---

## Adding Items to the Wishlist

There are two ways to add an item to your Wishlist:

1. **Manually** — while in Wishlist mode, tap the **+** button in the toolbar. A blank edit form opens. Fill in at least the Title and Artist, then tap Save.

2. **From MusicBrainz** — search MusicBrainz, open a release detail view, then tap the **heart (Add to Wishlist)** button in the toolbar. The item is added with full metadata and cover art. See [MusicBrainz Integration](musicbrainz.md#adding-to-your-wishlist-from-musicbrainz).

You can also right-click / long-press any MusicBrainz search result row and choose **Add to Wishlist** without opening the detail view.

---

## Moving a Wishlist Item to Your Collection

When you acquire an album on your Wishlist, move it to your collection in one of two ways:

- Open the item's detail view and tap **Add to Collection** in the toolbar.
- Right-click / long-press the item's row in the Wishlist list and choose **Add to Collection**.

The item is copied into your collection with all its metadata and cover art, then removed from the Wishlist. You can continue editing the resulting album entry to add tracks, credits, and tags.

---

## Wishlist on the Home Screen

If your Wishlist contains any items, a **Wishlist** coverflow section appears on the Home screen between the Recently Added and Spotlight sections. Tap any card to open that item's detail view. The number of items shown is configurable in Settings under **Wishlist Settings**.
