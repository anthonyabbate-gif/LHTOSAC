# Long Hill Township — Interactive Tax & Zoning Map

An interactive Leaflet map of Long Hill Township (Morris County, NJ) tax parcels,
colour-coded against the township's Open Space inventory. Parcel geometry and
attributes are pulled live from the NJ statewide parcel service; the open space
inventory is inlined in `index.html`.

## Pages

| Page | What it does |
|---|---|
| [`index.html`](./) | The main map — parcels, block labels, open space by owner type, Green Acres ROSI flagging, block highlighting, and a sortable table view |
| [`tools/block-expander.html`](./tools/block-expander.html) | Lists every lot a block contains and flags township-owned lots missing from the inventory |
| [`tools/block-14101-check.html`](./tools/block-14101-check.html) | Checks whether lot 17 in block 14101 is spelled `17.02` or `17.2` in the parcel service |
| [`tools/field-inspector.html`](./tools/field-inspector.html) | Reports which fields the parcel service actually returns, and which hold owner data |

## Open space inventory

Source: Long Hill Township Open Space Element of the Master Plan (17 December 2013),
revised per AbbateMapCritique3.

19 categories covering 396 parcels. Categories marked `provisional` render with a
dashed outline — they are parked for OSAC review rather than settled classifications.

## Green Acres ROSI

79 parcels are also on the township's Recreation and Open Space Inventory
(ROSI, February 2014 — fee simple; the conservation-restriction and lease pages of
that filing are empty). ROSI listing is a Green Acres **encumbrance**, not an
ownership category: listed land cannot be diverted or disposed of without NJDEP
approval. A parcel can therefore sit in any category *and* be on the ROSI.

The map carries this as a separate flag rather than a category — ROSI parcels take a
gold outline while keeping their category fill, so both read at once. The table has a
ROSI column with the park or facility name, and a "ROSI only" filter. Popups show
Green Acres encumbered acreage, which is less than the lot acreage where only part of
a lot is encumbered.

Matching is done on a normalised `block_Number(lot)` key, so the ROSI's `47.1` and the
inventory's `47.10` resolve to the same parcel.

**Four ROSI parcels were absent from the 2013 inventory** — `13102_1`, `10201_10.15`,
`11802_8.02` and `13702_6`. Green Acres encumbered land missing from the open space
inventory is a discrepancy for the committee, so they were added to `For OSAC Review`
rather than being assigned a category here.

### Settled

- **`14101_17.2`** — the lot-number spelling was queried against the parcel service
  and deliberately left as-is. Not an outstanding item.

### Unresolved

- **GSNWR staff housing and life rights** — on paper part of the refuge, physically
  ordinary residences. Pending verification with the refuge manager.
- **Digregorio (10301_13 / 10301_15)** — approved subdivision and donation that never
  happened. Pending check with the PZC.
- **Whole-block rows (items 30–33)** — "10403-10409 all", "10506 all", "10507 all".
  The township-owned lots already inventoried in those blocks were moved to
  Wetland/Floodplain. This was checked with the block expander and came back empty,
  but that check keys off the parcel service's owner field, which is currently
  returning no data — so an empty result proves nothing. **Re-run once the owner
  field is fixed.**
- **Schools (items 20–23)** — the open question is how to score partial open-space
  acreage per General Note 2B. A data-table issue, not a map recolour, so the map is
  unchanged.

## Data source

NJ Parcels Composite (`services2.arcgis.com`), filtered to `PCL_MUN = '1430'`.
The map queries it directly from the browser, so it needs network access at view time.
