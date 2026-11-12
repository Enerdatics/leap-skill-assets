# gis-map public layers

Reference layers for the Leap gis-map skill: GeoJSON (EPSG:4326, coordinates rounded to 5 decimals, about 1 m), one file per US state for lines and points.
`index.json` lists every file with its bytes, sha256, feature count and bounding box, plus each layer's source, licence, vintage, coverage and counts. Licences: see NOTICE; Enerdatics claims no copyright in these data files.

## Transmission lines

- Source: HIFLD Electric Power Transmission Lines (U.S. DHS HIFLD; data by Oak Ridge National Laboratory)
- Licence: Public domain (U.S. Government work, HIFLD/ORNL); modified by Enerdatics (clipped, simplified, fields reduced); some voltages inferred by HIFLD; no warranty
- Vintage: HIFLD Electric Power Transmission Lines; snapshot date not recorded in the extract (unproven)
- Coverage: AK, AL, AR, AZ, CA, CO, CT, DE, FL, GA, HI, IA, ID, IL, IN, KS, KY, LA, MA, MD, ME, MI, MN, MO, MS, MT, NC, ND, NE, NH, NJ, NM, NV, NY, OH, OK, OR, PA, RI, SC, SD, TN, TX, UT, VA, VT, WA, WI, WV, WY (no data for: DC, PR)
- Files: 50, features: 95,537
- Unique lines: 93,920; 1,582 cross a state border and appear, whole, in each of those state files (dedupe by `id`)
- Unknown voltage: 14.9% of lines (HIFLD -999999 or blank)
- Voltage bands (`kv_band`): `<100` under 100 kV, `100-161` 100 to 161 kV, `162-230` over 161 up to 230 kV, `231-345` over 230 up to 345 kV, `346-499` over 345 and under 500 kV, `500+` 500 kV and over, `unknown` voltage blank or <= 0 (HIFLD uses -999999)
- Status: In Service 73,022, Inactive 90, Not Available 20,779, Proposed 2, Under Construction 26. `planned` = Under Construction or Proposed; `inactive` = Inactive
- `type`: AC or DC where HIFLD states it, else blank. 4,044 lines below 69 kV are kept. A few HVDC lines carry the nominal voltage HIFLD publishes
- Simplified at 0.0005 degrees (about 55 m)

## State boundaries

- Source: U.S. Census Bureau cartographic boundary file (states)
- Licence: Public domain (U.S. Government work, U.S. Census Bureau); modified by Enerdatics (filtered to the 50 states, DC and Puerto Rico; simplified); no warranty
- Vintage: Census cartographic boundary file 2024, 1:5,000,000
- Coverage: AK, AL, AR, AZ, CA, CO, CT, DC, DE, FL, GA, HI, IA, ID, IL, IN, KS, KY, LA, MA, MD, ME, MI, MN, MO, MS, MT, NC, ND, NE, NH, NJ, NM, NV, NY, OH, OK, OR, PA, PR, RI, SC, SD, TN, TX, UT, VA, VT, WA, WI, WV, WY
- Files: 1, features: 52
- Simplified at 0.001 degrees (about 110 m)

## Not in this build

- Power plants: No power-plant input was supplied for this build.
- ISO/RTO boundaries (approximate): No ISO/RTO boundary input was supplied for this build.
