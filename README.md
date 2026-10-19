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

## Open space inventory

Source: Long Hill Township Open Space Element of the Master Plan (17 December 2013),
revised per AbbateMapCritique3.

19 categories covering 396 parcels. Categories marked `provisional` render with a
dashed outline — they are parked for OSAC review rather than settled classifications.

## Green Acres ROSI

Source: **NJDEP Office of Transactions and Public Land Administration, ROSI database
search for Morris County / Long Hill Twp, October 2026.** This replaced the February
2014 township filing in full.

202 unique entries, all Fee Simple, in three ownership types:

| Type | Entries | Matches the inventory | Facility |
|---|---|---|---|
| Municipal | 81 | **all 81** | 15 named facilities |
| County | 120 | none | Passaic River Park |
| Non-Profit | 1 | none | IMBIMBO - PRC |

ROSI listing is a Green Acres **encumbrance**, not an ownership category: listed land
cannot be diverted or disposed of without NJDEP approval, and a parcel can sit in any
category *and* be on the ROSI. The map carries it as a separate flag — ROSI parcels
take a gold outline while keeping their category fill. The table has a ROSI column
with the facility name and a "ROSI only" filter; popups show the interest and
ownership type.

### The county numbering gap

Only the 81 Municipal entries use Long Hill's 5-digit tax blocks. The 120 County and
1 Non-Profit entries are numbered in a different scheme — blocks `1`, `18`, `171`–`177`,
some with decimals such as `171.30` — matching nothing in the township tax map. They
will never match a parcel and never render on the map. **They are kept in the data
verbatim rather than dropped**, because they are part of the filing and the gap is a
real discrepancy to reconcile with NJDEP.

48 of the 120 County entries have a lot number that coincides with some County parcel
in the inventory (filed `blk 1 lot 10.21` against the inventory's `10201_10.21`), which
hints at a crosswalk. The blocks genuinely differ, and several filed lots match more
than one inventory block, so no crosswalk has been guessed. NJDEP's own disclaimer
applies: *"The tax block and lot numbering of properties listed on the ROSI may have
changed since the ROSI was submitted."*

### What changed from the 2014 filing

Against the 79 municipal parcels of the 2014 filing: 75 carried over, 6 added, 4 dropped.
Three of the four drops pair with an added lot in the same block — `10201_10.15` →
`10201_10.14`, `11802_8.02` → `11802_1`, `13702_6` → `13702_5` — which reads as NJDEP
correcting lot numbers rather than parcels leaving the ROSI. Those three were in
`For OSAC Review` precisely because the old filing listed them and the inventory did
not; they are probably artifacts and are annotated as such, pending the committee.
`13102_1` (Stirling Lake) is still ROSI-listed and remains a genuine gap.

**Acreage is gone.** The NJDEP export carries Block, Lot, Facility, Interest and Type
only. The Green Acres encumbered acreage the 2014 filing provided, and its partial-lot
markers, are no longer available.

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
