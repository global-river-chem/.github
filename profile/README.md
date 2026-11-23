# Global River Chemistry

We are bringing together river chemistry, discharge, watershed boundaries, and environmental data from rivers around the world. The goal is to understand what controls river silicon, compare patterns across sites, and make better predictions for rivers that are not regularly monitored.

This work is supported by the John Wesley Powell Center for Analysis and Synthesis and NSF Using Long-Term Research Associated Data (ULTRA-Data). It grew out of the River Si working group started through the NCEAS LTER network.

## The short version

Everything starts with the site reference table. Each river site gets one checked name and ID, and the chemistry, discharge, watershed, and spatial data all link back to that record.

We leave the original downloads alone. If something needs to be corrected or left out of a processed dataset, we keep the original value and record what we changed, why we changed it, and which source we checked.

New data do not go straight into the main datasets. We check the site match, chemistry, discharge, watershed, and spatial results first. When those pieces are ready, the site can be added to a new dated release.

```text
Published source data
        |
        v
Site reference table
identity, coordinates, waterbody, source links, and release decisions
        |
        +------------------------------+
        |                              |
        v                              v
Chemistry and discharge          Watershed review
standardization and QA/QC        and boundary selection
        |                              |
        v                              v
Dated chemistry and              Environmental data extraction
discharge master datasets        and spatial QA/QC
        |                              |
        +---------------+--------------+
                        |
                        v
               Checked project releases
                        |
                        v
             Shiny app, WRTDS, and DSi models
```

## Repositories

| Repository | What it is for |
| --- | --- |
| [data-workflow_disc-chem](https://github.com/global-river-chem/data-workflow_disc-chem) | Downloads, checks, and combines the chemistry and discharge data |
| [data-workflow_spatial](https://github.com/global-river-chem/data-workflow_spatial) | Checks watersheds, extracts environmental data, and builds the spatial tables |
| [global-river-chem-shiny](https://github.com/global-river-chem/global-river-chem-shiny) | Runs the interactive maps and plots |
| [dsi-unmonitored](https://github.com/global-river-chem/dsi-unmonitored) | Fills gaps and predicts monthly dissolved silicon |
| [ESOM](https://github.com/global-river-chem/ESOM) | Brings the checked spatial data into the ESOM work |
| [lterwg-silica-data](https://github.com/lter/lterwg-silica-data) | Contains the working-group analyses, current WRTDS work, and earlier chemistry workflow |
| [lterwg-silica-spatial](https://github.com/lter/lterwg-silica-spatial) | Contains the earlier AppEEARS and spatial extraction workflow |

## Main parts of the project

### Site reference

The [site reference table](https://docs.google.com/spreadsheets/d/11t9YYTzN_T12VAQhHuY5TpVjGS50ymNmKznJK4rKTIU/edit) is where the pieces come together. It keeps track of site names and aliases, chemistry and discharge locations, drainage areas, watershed files, source links, and whether a site is ready for a release.

The main datasets are for rivers, streams, creeks, brooks, approved canals, and tidal river channels. Lakes, soil water, and other non-stream sites are kept separately. New sites stay in the pending files until we have checked the data needed to move them into the main dataset.

### Chemistry and discharge

The [chemistry and discharge workflow](https://github.com/global-river-chem/data-workflow_disc-chem) gets the latest published data and puts the different sources into the same basic format. It checks site matches, units, dates, detection limits, qualifiers, and records that overlap across sources.

The original downloads do not get edited. A usable value can stay in the main dataset with a flag if it needs context. We only leave a value out when there is a clear reason, and we save that reason with the processed data.

### Watersheds and spatial data

The [spatial workflow](https://github.com/global-river-chem/data-workflow_spatial) checks the watershed boundary for each site. If a reliable boundary is not already available, we derive one and review it. The workflow then extracts the environmental data for that watershed and builds the GlASS and ERA5-Land tables.

The spatial data cover climate, snow, vegetation, land cover, atmospheric deposition, soils, lithology, permafrost, population, dams, and wastewater. Each result stays linked to the watershed and source version used to create it. The [spatial product guide](https://github.com/global-river-chem/data-workflow_spatial/blob/main/docs/data-products/README.md) lists the products, years, units, and shared folders.

### What we check before a release

We use `LTER` and `Stream_Name` together to match a site across the chemistry, discharge, reference, watershed, and spatial files. We keep IDs as text so leading zeroes do not disappear.

Before a site goes into a main release, we make sure we have checked:

- site identity and aliases
- waterbody type and sampling coordinates
- chemistry and discharge source matches
- duplicate records and overlapping data sources
- units, qualifiers, methods, and dates
- watershed location and drainage area
- spatial extraction coverage and unusual values
- links to the exact source data and saved watershed files

## Where the shared files are

| Project area | Shared folder or workbook |
| --- | --- |
| Current spatial datasets | [GlASS, ERA5-Land, metadata, and dictionary](https://drive.google.com/drive/folders/1dh2uxghBGCeYZZZiBIuA407yzNAcR-9O) |
| Individual spatial products | [Source files and extracted results by product](https://drive.google.com/drive/folders/15GVMkhS1a5ynqSUCPuloViKyar4frQGU) |
| Earlier spatial releases | [Archived spatial datasets](https://drive.google.com/drive/folders/1ELbbxbed1YZr0oM61e89_Aia6uSZ6c6r) |
| Chemistry source files | [Chemistry files](https://drive.google.com/drive/folders/1da8AkSvforPehp-gPJsmA7-pPAJ913mz) |
| Discharge source files | [Discharge files](https://drive.google.com/drive/folders/1mw0rYbqpMO4VIXfTH5Ry9USzlR4tbvfb) |
| Watershed boundaries | [Current, pending, unmatched, and earlier shapefiles](https://drive.google.com/drive/folders/1TLEFKLWUpTKwxKiZv9nqhdwccflPuF9g) |
| Site reference | [Site identity, locations, sources, and release decisions](https://docs.google.com/spreadsheets/d/11t9YYTzN_T12VAQhHuY5TpVjGS50ymNmKznJK4rKTIU/edit) |
| Laboratory metadata | [Methods, fractions, units, and workflow rules](https://docs.google.com/spreadsheets/d/1PshqCYF2hAR9WhpgN65KLBm0qiqcBmihwkGdSesxI3Q/edit) |

GitHub holds the code, checks, settings, and documentation. Google Drive and Box hold the large files, including the original downloads, shapefiles, extraction results, review files, and dated master datasets. Google Sheets holds the site reference and laboratory metadata.

Large data files and credentials stay out of GitHub. Each dated release should include enough information to understand where the data came from, what the units are, what is covered, and what changed during QA/QC.

## What uses these data

- The [Global River Chemistry Shiny app](https://github.com/global-river-chem/global-river-chem-shiny) is a quick way to explore the checked chemistry, discharge, and spatial data
- The [DSi prediction workflow](https://github.com/global-river-chem/dsi-unmonitored) fills gaps, extends time series, and predicts dissolved silicon for rivers without regular monitoring
- The [ESOM workflow](https://github.com/global-river-chem/ESOM) brings the checked spatial products into the ESOM analysis
- WRTDS uses sites with enough overlapping chemistry and discharge data that have also passed the eligibility checks

## Where this started

The original working-group repositories are still available:

- [Original chemistry and analysis repository](https://github.com/lter/lterwg-silica-data)
- [Original spatial extraction repository](https://github.com/lter/lterwg-silica-spatial)

The newer repositories split the work into chemistry and discharge, spatial extraction, visualization, and prediction. That makes it easier to update one part of the project without touching the original data or rebuilding everything else.
