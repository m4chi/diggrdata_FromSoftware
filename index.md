# diggrdata_FromSoftware

This site features the interactive and non-interactive visualizations created based on the datasets about videogames developed and or published by the Japanese company FromSoftware stored in this repository. For more informations, see the [README](README.md)
The data is used in my ongoing research project on videogame spatialization, and will be updated and extended over time. For stable versions used in my research, please refer to the Zenodo upload specified in the respective research output.


## 1. FromSoftware Production

### 1.1. FromSoftware Collaborators per game per country

### 1.2. FromSoftware Production Network based on Mobygames Release Data

Production network of companies involved in FromSoftware games according to the release data on Mobygames.com. Edges are based on contribution to the same game (collaboration network), including a distinction of node for different roles a company might take on, as well as the company location if available via Wikidata. The data was created with [diggr lemongrab](https://github.com/diggr/lemongrab) and edited manually in Gephi 0.9.2 to add statistical data, as well as to include several country data missing on Wikidata and a country based color hex code, following this color schema:

![this hex color schema](visualizations/FromSoftCountryColorCodesTable.png)


## 2. FromSoftware Distribution

### 2.1. Distribution Overview

### 2.2. Release Timeline

[Release timeline](visualizations/fromsoft_release_release_timeline.md)


All available FromSoftware game releases in Japan (JP), Europe (EU) and North America (US) mapped on an interactive timeline with some additional information. The visualization was created with [diggr tulpa](https://github.com/diggr/tulpa). Provenance information is available, added with [diggr provit](https://github.com/diggr/provit).

## 4. Various visualizations and charts created from the data between October 2020 and December 2020

1. [Headquarter Locations of Companies involved in FromSoftware games](visualizations/FromSoftware_ReleaseAnalysis_CompanyLocations.svg)
2. [Distribution of first releases by region](visualizations/FromSoftware_ReleaseAnalysis_FirstReleaseCountryDistribution.svg)
3. [Temporal Distance between first release in Japan and first release in the US and EU region](visualizations/FromSoftware_ReleaseAnalysis_ReleaseDistanceJPEUUS.svg)
4. [Per-game releases per region, stacked](visualizations/FromSoftware_ReleaseAnalysis_ReleaseRegion.svg)
5. [Role-based chart of company locations, divided into two groups, a.) Japan, b.) other countries](visualizations/FromSoftware_Rolebased_companyCountries.svg)

# Meta

**License**
[CC-BY 4.0](http://creativecommons.org/licenses/by/4.0)
![license](https://i.creativecommons.org/l/by/4.0/80x15.png)

**Copyright**
2021 Martin Roth [research@asobiba.de](mailto: research@asobiba.de)
