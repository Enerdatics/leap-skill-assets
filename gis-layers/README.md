# gis-map public layers

Reference layers for the Leap gis-map skill: GeoJSON (EPSG:4326, coordinates rounded to 5 decimals, about 1 m), one file per US state for lines and points.
`index.json` lists every file with its bytes, sha256, feature count and bounding box, plus each layer's source, licence, vintage, coverage and counts. Licences: see NOTICE; Enerdatics claims no copyright in these data files.

## Transmission lines

- Source: HIFLD Electric Power Transmission Lines (U.S. DHS HIFLD; data by Oak Ridge National Laboratory)
- Licence: Public domain (U.S. Government work, HIFLD/ORNL); modified by Enerdatics (clipped, simplified, fields reduced); some voltages inferred by HIFLD; no warranty
- Vintage: HIFLD Electric Power Transmission Lines; snapshot date not recorded in the extract (unproven)
- Coverage: AK, AL, AR, AZ, CA, CO, CT, DE, FL, GA, HI, IA, ID, IL, IN, KS, KY, LA, MA, MD, ME, MI, MN, MO, MS, MT, NC, ND, NE, NH, NJ, NM, NV, NY, OH, OK, OR, PA, RI, SC, SD, TN, TX, UT, VA, VT, WA, WI, WV, WY (no data for: DC, PR)
- Files: 50, features: 95,537
- Files unchanged since commit `589053ebaa4b8514f5bdb185620b5b84eaa58058` of this repository and served from it (`ref` in index.json); they are not in this folder. The sha256 values above still apply
- Unique lines: 93,920; 1,582 cross a state border and appear, whole, in each of those state files (dedupe by `id`)
- Unknown voltage: 14.9% of lines (HIFLD -999999 or blank)
- Voltage bands (`kv_band`): `<100` under 100 kV, `100-161` 100 to 161 kV, `162-230` over 161 up to 230 kV, `231-345` over 230 up to 345 kV, `346-499` over 345 and under 500 kV, `500+` 500 kV and over, `unknown` voltage blank or <= 0 (HIFLD uses -999999)
- Status: In Service 73,022, Inactive 90, Not Available 20,779, Proposed 2, Under Construction 26. `planned` = Under Construction or Proposed; `inactive` = Inactive
- `type`: AC or DC where HIFLD states it, else blank. 4,044 lines below 69 kV are kept. A few HVDC lines carry the nominal voltage HIFLD publishes
- Simplified at 0.0005 degrees (about 55 m)

## Natural gas pipelines (operating)

- Source: U.S. Energy Information Administration, Natural Gas Interstate and Intrastate Pipelines map layer (https://www.eia.gov/maps/map_data/NaturalGas_InterIntrastate_Pipelines_US_EIA.zip)
- Licence: Public domain (U.S. Government work, U.S. Energy Information Administration); modified by Enerdatics (operating segments only, filed by state, simplified, fields reduced); no warranty
- Vintage: Jan 2020
- Coverage: AK, AL, AR, AZ, CA, CO, CT, DE, FL, GA, IA, ID, IL, IN, KS, KY, LA, MA, MD, ME, MI, MN, MO, MS, MT, NC, ND, NE, NH, NJ, NM, NV, NY, OH, OK, OR, PA, RI, SC, SD, TN, TX, UT, VA, VT, WA, WI, WV, WY (no data for: DC, HI, PR)
- Files: 49, features: 33,646
- Operating segments: 32,907 (Gathering 69 segments / 4,100 km, Interstate 17,959 segments / 245,667 km, Intrastate 14,879 segments / 120,866 km); 728 touch more than one state and appear, whole, in each of those state files (dedupe by `id`)
- `offshore`: 1,093 segments touch no (coast-clipped) state polygon and are filed under the nearest state. Basis: touches no US state polygon and no non-US land polygon (countries input)
- Dropped as lying on non-US land only (Canada, Mexico): 0
- `id` is the segment's row number in the EIA file: stable within one release, not across releases
- No capacity or diameter: EIA's layer carries only pipe type, operator and status. `length_km` is geodesic, measured before simplification
- Planned pipelines are not in this layer (see the planned pipelines layer, if present)
- Simplified at 0.0005 degrees (about 55 m)

## Natural gas pipelines (planned: proposed and under construction)

- Source: Global Energy Monitor, Global Gas Infrastructure Tracker (US subset) (https://globalenergymonitor.org/)
- Licence: CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/)
- Attribution (required): Global Energy Monitor, Global Gas Infrastructure Tracker, CC BY 4.0
- Not a federal source; routes approximate.
- Modified by Enerdatics: US proposed and under-construction pipelines only; filed by state; simplified; fields reduced and renamed; lengths computed; no warranty
- Vintage: GEM Global Gas Infrastructure Tracker; release date not recorded in the extract (unproven)
- Coverage: AK, AL, AZ, CO, FL, GA, ID, IL, LA, MN, MS, NC, ND, NM, NV, OH, PA, TN, TX, VA, WI, WY (no data for: AR, CA, CT, DC, DE, HI, IA, IN, KS, KY, MA, MD, ME, MI, MO, MT, NE, NH, NJ, NY, OK, OR, PR, RI, SC, SD, UT, VT, WA, WV)
- Files: 22, features: 74
- Features: 57 (40 proposed, 17 under construction; `planned` = 1); 15 touch more than one state and appear, whole, in each of those state files (dedupe by `id`). One project can be several features
- `capacity_bcm_y`: GEM capacity in bcm/y, blank for 9 features
- `id` is the feature's row number in the GEM extract (it has no GEM project id): stable within one extract, not across releases
- Simplified at 0.0005 degrees (about 55 m)

## Existing conventional power plants (EIA-860M)

- Source: U.S. Energy Information Administration, Form EIA-860M Preliminary Monthly Electric Generator Inventory (September 2026), Operating and Planned tabs incl. Puerto Rico (https://www.eia.gov/electricity/data/eia860m/)
- Licence: Public domain. Source: U.S. Energy Information Administration, Form EIA-860M (September 2026)
- Modified by Enerdatics: generator rows aggregated to one point per plant and status (operating / planned); conventional plants only (plants mainly solar, wind or battery storage left out); retired and canceled generators excluded; fields reduced; coordinates rounded; no warranty
- Vintage: EIA-860M, September 2026 (generator inventory as of that month)
- Coverage: AK, AL, AR, AZ, CA, CO, CT, DC, DE, FL, GA, HI, IA, ID, IL, IN, KS, KY, LA, MA, MD, ME, MI, MN, MO, MS, MT, NC, ND, NE, NH, NJ, NM, NV, NY, OH, OK, OR, PA, PR, RI, SC, SD, TN, TX, UT, VA, VT, WA, WI, WV, WY
- Files: 52, features: 5,460
- Plants: 5,289 operating, 171 planned (`status`); one point per plant and status, aggregated from EIA-860M generator rows. A plant with a planned expansion appears once per status
- Conventional only: solar, wind and battery plants excluded (11,014 plants whose largest share of nameplate MW is solar, wind or battery storage, even if they also have a conventional unit)
- `nameplate_mw` and `generators` count only a plant's conventional units; `has_renewable_units` = it also has solar, wind or battery units, not counted (93 plants)
- 3 planned points belong to a plant whose operating part was excluded, so they have no operating twin
- Generator rows read: 31,073; dropped for unusable coordinates or state: 0. Retired and canceled/postponed generators are not included
- `fuel_category` (for styling; the plant's largest category by nameplate MW): `gas` 2,120, `coal` 193, `nuclear` 58, `hydro` 1,471, `oil` 900, `geothermal` 70, `biomass` 593, `other` 55
- `planned_operation`: earliest planned operation year-month of a planned plant's generators
- In a different state's polygon than stated (kept, flagged `state_mismatch`): 26
- A plant can also appear as a Leap project

## State boundaries

- Source: U.S. Census Bureau cartographic boundary file (states)
- Licence: Public domain (U.S. Government work, U.S. Census Bureau); modified by Enerdatics (filtered to the 50 states, DC and Puerto Rico; simplified); no warranty
- Vintage: Census cartographic boundary file 2024, 1:5,000,000
- Coverage: AK, AL, AR, AZ, CA, CO, CT, DC, DE, FL, GA, HI, IA, ID, IL, IN, KS, KY, LA, MA, MD, ME, MI, MN, MO, MS, MT, NC, ND, NE, NH, NJ, NM, NV, NY, OH, OK, OR, PA, PR, RI, SC, SD, TN, TX, UT, VA, VT, WA, WI, WV, WY
- Files: 1, features: 52
- Simplified at 0.001 degrees (about 110 m)

## Not in this build

- ISO/RTO boundaries (approximate): No ISO/RTO boundary input was supplied for this build.
