# diggrdata_FromSoftware

This site augments my publications on the spatialization of videogame production, distribution and reception in the case of the Japanese company FromSoftware.
This research is currently published or accepted for publication as follows:
Roth, Martin (ロート　マーティン). Accepted, 2021. テレビゲーム文化の空間的展開：FromSoftwareゲームの生産的・流通的展開とそれにおけるソフトな文化的境界線. [Replaying Japan](https://www.rcgs.jp/?page_id=200), Vol. 3.

The site features interactive and non-interactive visualizations used for or resulting from my analysis of the data stored in the [diggrdata_FromSoftware repository](https://github.com/m4chi/diggrdata_FromSoftware). For more information, see the [README](README.md).
The data is used in my ongoing research project on videogame spatialization, and will be updated and extended over time. For stable versions used in my research, please refer to the Zenodo snapshot specified in the respective research output.


## 1. FromSoftware Production

### 1.1. FromSoftware Collaborators per game per country

The following figures provide an overview of the companies involved in the production of FromSoftware games, based on datasets [1. FromSoftware DataTable](/data/FromSoftware_Tulpa_DataTable_edited20210105.csv) and [2. FromSoftware Production Network based on Mobygames Release Data](/data/). Click on the image for a higher resolution version.

[![Headquarter Locations of Companies involved in FromSoftware games](visualizations/FromSoftware_ReleaseAnalysis_CompanyLocations.svg)](visualizations/FromSoftware_ReleaseAnalysis_CompanyLocations.svg)

[![Role-based chart of company locations, divided into two groups, a.) Japan, b.) other countries](visualizations/FromSoftware_Rolebased_companyCountries.svg)](visualizations/FromSoftware_Rolebased_companyCountries.svg)

### 1.2. FromSoftware Production Network based on Mobygames Release Data

The following figures depict the production networks of companies involved in FromSoftware games according to the release data on Mobygames.com, based on the dataset 2. FromSoftware Production Network [nodelist](/data/FromSoftware_ProductionNetwork_MobygamesReleaseBased20201005_nodes.csv) and [edgelist](/data/FromSoftware_ProductionNetwork_MobygamesReleaseBased20201005_edges.csv). Edges are based on contribution to the same game (collaboration network). Nodes are defined for each company in each distinct role it takes on. Company location was added where available via Wikidata. The data was created with [diggr lemongrab](https://github.com/diggr/lemongrab) and edited manually in Gephi 0.9.2 to add statistical data, as well as to include several country data missing on Wikidata and a country based color hex code, following this color schema:

![this hex color schema](visualizations/FromSoftCountryColorCodesTable.png)

This network visualization shows all actors, meaning any companies in any role involved in producing a FromSoftware game.

[![FromSoftware Production Network, all collaborators](visualizations/FromSoftware_ProductionNetwork_withroles_all.svg)](visualizations/FromSoftware_ProductionNetwork_withroles_all.svg)

This network visualization excludes the actors who take on functions needed when publishing a game outside of Japan, such as "localization."

[![FromSoftware Production Network, limited collaborators](visualizations/FromSoftware_ProductionNetwork_withroles_nopubldistrloc.svg)](visualizations/FromSoftware_ProductionNetwork_withroles_nopubldistrloc.svg)


## 2. FromSoftware Distribution

### 2.1. Distribution Overview

The following visualizations show the historical change in the regional distribution of FromSoftware games. They are based on the dataset [1. FromSoftware DataTable](/data/FromSoftware_Tulpa_DataTable_edited20210105.csv) and [3. FromSoftware Release Data](/data/FromSoftware_releases.json).

Number of releases per region per game
[![Per-game releases per region, stacked](visualizations/FromSoftware_ReleaseAnalysis_ReleaseRegion.svg)](visualizations/FromSoftware_ReleaseAnalysis_ReleaseRegion.svg)

First release region distribution
[![Distribution of first releases by region](visualizations/FromSoftware_ReleaseAnalysis_FirstReleaseCountryDistribution.svg)](visualizations/FromSoftware_ReleaseAnalysis_FirstReleaseCountryDistribution.svg)

Temporal distance between first release in Japan and first release in US and EU
[![Temporal Distance between first release in Japan and first release in the US and EU region](visualizations/FromSoftware_ReleaseAnalysis_ReleaseDistanceJPEUUS.svg)](visualizations/FromSoftware_ReleaseAnalysis_ReleaseDistanceJPEUUS.svg)

### 2.2. Release Timeline

The following link takes you to an interactive visualization of all available FromSoftware game releases in Japan (JP), Europe (EU) and North America (US) mapped on a timeline with various additional information about each game. The visualization was created with [diggr tulpa](https://github.com/diggr/tulpa). Provenance information is available, added with [diggr provit](https://github.com/diggr/provit).

[Interactive Release Timeline](visualizations/fromsoft_release_release_timeline.html)

# Meta

**License**
[CC-BY 4.0](http://creativecommons.org/licenses/by/4.0)
![license](https://i.creativecommons.org/l/by/4.0/80x15.png)

**Copyright**
2021 Martin Roth [research@asobiba.de](mailto: research@asobiba.de)
