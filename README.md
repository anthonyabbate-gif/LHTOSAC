# Long Hill Township — Interactive Tax & Zoning Map

An interactive Leaflet map of Long Hill Township (Morris County, NJ) tax parcels,
colour-coded against the township's Open Space inventory. Parcel geometry and
attributes are pulled live from the NJ statewide parcel service; the open space
inventory is inlined in `index.html`.

## Pages

| Page | What it does |
|---|---|
| [`index.html`](./) | The main map — parcels, block labels, open space by owner type, block highlighting, and a sortable table view |
| [`tools/block-expander.html`](./tools/block-expander.html) | Lists every lot a block contains and flags township-owned lots missing from the inventory |
| [`tools/block-14101-check.html`](./tools/block-14101-check.html) | Checks whether lot 17 in block 14101 is spelled `17.02` or `17.2` in the parcel service |

## Open space inventory

Source: Long Hill Township Open Space Element of the Master Plan (17 December 2013),
revised per AbbateMapCritique3.

19 categories covering 392 parcels. Categories marked `provisional` render with a
dashed outline — they are parked for OSAC review rather than settled classifications.

### Settled

- **`14101_17.2`** — the lot-number spelling was queried against the parcel service
  and deliberately left as-is. Not an outstanding item.
- **Whole-block rows (items 30–33)** — "10403-10409 all", "10506 all", "10507 all".
  The township-owned lots already inventoried in those blocks were moved to
  Wetland/Floodplain, and that was reviewed against the parcel service and found
  complete. No further lots to enumerate.

### Unresolved

- **GSNWR staff housing and life rights** — on paper part of the refuge, physically
  ordinary residences. Pending verification with the refuge manager.
- **Digregorio (10301_13 / 10301_15)** — approved subdivision and donation that never
  happened. Pending check with the PZC.
- **Schools (items 20–23)** — the open question is how to score partial open-space
  acreage per General Note 2B. A data-table issue, not a map recolour, so the map is
  unchanged.

## Data source

NJ Parcels Composite (`services2.arcgis.com`), filtered to `PCL_MUN = '1430'`.
The map queries it directly from the browser, so it needs network access at view time.
