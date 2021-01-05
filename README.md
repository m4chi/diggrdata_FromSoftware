# diggrdata_FromSoftware

This repository features several datasets about videogames developed and or published by the Japanese company FromSoftware. The data is used in my ongoing research project on videogame spatialization, and will be updated and extended over time. For stable versions used in my research, please refer to the Zenodo upload specified in the respective research output.

Large portions of the data have been aggregated with the [diggr tools](https://github.com/diggr/) and edited manually thereafter. This research has received support from the DFG.

This readme provides an overview of the data included in this dataset.

## FromSoftware Datatable

### current version from

2021-01-05

### filename

FromSoftware_Tulpa_DataTable_edited20210105.csv

### content summary

This file contains data found on Mobygames.com, Wikidata and GameFAQs for a manually curated set of videogame titles including all known games developed by the Japanese developer and publisher FromSoftware. The data includes
- the number of releases per release region 
- the number of companies per country involved in the production
- identifier data for Mobygames.com

The original data was created based on our curated dataset  with [diggr tulpa](https://github.com/diggr/tulpa). It was then edited to include an all-english game title version, as well as some aggregate information. The column names were changed in some cases to be more self-explanatory.

### column description

title
- title of the game according to our curated list

edited title	
- title in roman letters only, for convenience reasons

first_release_year
- year of the first release of a game, used for sorting

xx_releases (multiple columns)
- number of releases for several release regions, including 
  - AS (Asia)
  - AU (Australia)
  - EU (Europe)
  - JP (Japan)
  - KO (Korea)
  - US (North America).

n_releases
- number of releases in total

columns named after countries (multiple columns)
- number of companies contributing to a game having their headquarters in the respective country according to Wikidata
  
Non-Japan based companies
- aggregate of companies with headquarters outside of Japan

n_companies	
- total number of companies

platforms	
- all platforms a game has been published for

unknown
- number of companies involved with unknown headquarter location

moby_id	
- id of the mobygames data on a game

moby_slug	
- slug of the mobygames data on a game

moby_title
- title used on mobygames for a game
