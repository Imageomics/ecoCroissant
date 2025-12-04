# ecoCroissant Specification

## Croissant Extension for Biodiversity Metadata

Version 1.0

<http://imageomics.org/ecoCroissant/1.0>

## Introduction

ecoCroissant is an extension to the [Croissant format](http://mlcommons.org/croissant/1.0) designed to capture ecologically-relevant information from biodiversity datasets. It follows [FAIR4AI principles](https://www.nature.com/articles/s41597-022-01759-2) to ensure datasets are Findable, Accessible, Interoperable, and Reusable for AI/ML applications in ecological and biodiversity research.

Biodiversity datasets contain unique characteristics that are not adequately captured by the base Croissant format, including:

- **Taxonomic information**: Species identification, taxonomic hierarchy, and nomenclature
- **Geographic and temporal context**: Collection locations, habitats, and temporal coverage
- **Ecological relationships**: Trophic levels, species interactions, and ecological roles
- **Collection methodology**: Observation methods, specimen handling, and data quality indicators
- **Conservation context**: IUCN status, protected areas, and population data

The ecoCroissant extension addresses these needs by providing a standardized vocabulary for documenting ecological and biodiversity metadata in ML-ready datasets.

## Prerequisites

The ecoCroissant vocabulary builds on the [schema.org/Dataset](http://schema.org/Dataset) vocabulary and the [Croissant core vocabulary](http://mlcommons.org/croissant/1.0).

### Namespace

The ecoCroissant vocabulary is defined in its own namespace, identified by the IRI:

```
http://imageomics.org/ecoCroissant/
```

We abbreviate this namespace IRI using the prefix `eco`.

### Related Vocabularies

ecoCroissant integrates with established biodiversity standards:

| Prefix | IRI | Description |
|--------|-----|-------------|
| sc | http://schema.org/ | The schema.org namespace |
| cr | http://mlcommons.org/croissant/ | MLCommons Croissant namespace |
| dwc | http://rs.tdwg.org/dwc/terms/ | Darwin Core terms |
| gbif | https://www.gbif.org/species/ | GBIF Species API |
| ncbi | https://www.ncbi.nlm.nih.gov/taxonomy/ | NCBI Taxonomy |
| eol | https://eol.org/pages/ | Encyclopedia of Life |
| iucn | https://www.iucnredlist.org/ | IUCN Red List |

### Conformance

ecoCroissant datasets must declare conformance to this specification:

```json
"dct:conformsTo": "http://imageomics.org/ecoCroissant/1.0"
```

## Use Cases

### Use Case 1: Taxonomic Discovery and Classification

ML models for species identification require rich taxonomic context. ecoCroissant enables:

- **Hierarchical taxonomy**: Complete taxonomic lineage from kingdom to subspecies
- **Taxonomic identifiers**: Links to authoritative databases (GBIF, NCBI, EOL)
- **Nomenclature history**: Synonyms, basionyms, and taxonomic revisions
- **Vernacular names**: Common names across languages and regions

### Use Case 2: Geographic and Habitat Context

Ecological datasets require spatial and habitat information:

- **Geolocation**: Coordinates with precision and datum information
- **Habitat classification**: Biome, ecosystem, and microhabitat descriptions
- **Elevation and depth**: Altitude/depth ranges for species occurrences
- **Protected areas**: National parks, reserves, and conservation zones

### Use Case 3: Temporal Ecology

Understanding temporal patterns in biodiversity data:

- **Seasonality**: Phenological timing, migration patterns
- **Collection timeline**: When observations or specimens were collected
- **Historical context**: Changes in distribution or abundance over time

### Use Case 4: Species Interactions and Ecology

Capturing ecological relationships:

- **Trophic relationships**: Predator-prey, herbivore-plant interactions
- **Symbiotic relationships**: Mutualism, parasitism, commensalism
- **Pollination and dispersal**: Plant-animal interactions
- **Ecological roles**: Keystone species, ecosystem engineers

### Use Case 5: Conservation and Population Status

Conservation-relevant metadata:

- **IUCN Red List status**: Global and regional threat assessments
- **Population trends**: Increasing, stable, decreasing
- **Threats**: Habitat loss, climate change, invasive species
- **Protection status**: Legal protection levels

### Use Case 6: Data Quality and Provenance

Ensuring data reliability for ML applications:

- **Identification confidence**: Expert-verified vs. citizen science observations
- **Data collection method**: Field observation, museum specimen, remote sensing
- **Georeferencing quality**: GPS accuracy, geocoding method
- **Temporal precision**: Exact date vs. date range

## ecoCroissant Properties

### Taxonomic Properties

| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:taxon | sc:Taxon or sc:Text | MANY | The taxonomic name(s) of organisms in the dataset |
| eco:taxonRank | sc:Text | ONE | The taxonomic rank (e.g., species, genus, family) |
| eco:scientificName | sc:Text | ONE | The full scientific name including authorship |
| eco:taxonID | sc:URL | MANY | Identifier(s) from taxonomic databases (GBIF, NCBI, etc.) |
| eco:higherClassification | sc:Text | ONE | Full taxonomic hierarchy (Kingdom > Phylum > Class > Order > Family > Genus > Species) |
| eco:vernacularName | sc:Text | MANY | Common name(s) in various languages |
| eco:taxonomicStatus | sc:Text | ONE | Status of the taxon name (accepted, synonym, etc.) |

### Geographic Properties

| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:locality | sc:Text | ONE | Description of the location |
| eco:habitat | sc:Text | MANY | Habitat type(s) where organisms occur |
| eco:biome | sc:Text | ONE | Major biome classification |
| eco:continent | sc:Text | ONE | Continent of occurrence |
| eco:country | sc:Text | MANY | Country/countries of occurrence |
| eco:coordinateUncertaintyInMeters | sc:Number | ONE | Uncertainty radius for coordinates |
| eco:minimumElevationInMeters | sc:Number | ONE | Minimum elevation of occurrences |
| eco:maximumElevationInMeters | sc:Number | ONE | Maximum elevation of occurrences |
| eco:minimumDepthInMeters | sc:Number | ONE | Minimum depth (for aquatic organisms) |
| eco:maximumDepthInMeters | sc:Number | ONE | Maximum depth (for aquatic organisms) |

### Temporal Properties

| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:eventDate | sc:Date or sc:DateTime | MANY | Date(s) when data was collected |
| eco:eventDateStart | sc:Date | ONE | Start of collection period |
| eco:eventDateEnd | sc:Date | ONE | End of collection period |
| eco:seasonality | sc:Text | MANY | Seasonal patterns in the data |
| eco:lifeStage | sc:Text | MANY | Life stage(s) represented (egg, larva, adult, etc.) |

### Ecological Properties

| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:trophicLevel | sc:Text | ONE | Position in food chain (producer, primary consumer, etc.) |
| eco:ecologicalRole | sc:Text | MANY | Ecological function (pollinator, predator, decomposer, etc.) |
| eco:speciesInteractions | sc:Text | MANY | Description of species interactions in the dataset |
| eco:diet | sc:Text | MANY | Diet composition for animals |
| eco:hostOrganism | sc:Text | MANY | Host species (for parasites, symbionts) |

### Conservation Properties

| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:iucnStatus | sc:Text | ONE | IUCN Red List category (LC, NT, VU, EN, CR, EW, EX) |
| eco:iucnStatusSource | sc:URL | ONE | Link to IUCN assessment |
| eco:populationTrend | sc:Text | ONE | Population trend (increasing, stable, decreasing, unknown) |
| eco:threats | sc:Text | MANY | Known threats to the species |
| eco:conservationActions | sc:Text | MANY | Conservation actions in place or recommended |
| eco:protectedArea | sc:Text | MANY | Protected areas where species occurs |

### Data Quality Properties

| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:identificationVerificationStatus | sc:Text | ONE | Verification level of taxonomic identifications |
| eco:identifiedBy | sc:Text | MANY | Who identified the specimens/observations |
| eco:samplingProtocol | sc:Text | ONE | Method used to collect data |
| eco:dataGeneralizations | sc:Text | ONE | Any data generalizations applied (e.g., coordinate obscuring) |
| eco:informationWithheld | sc:Text | ONE | Information intentionally withheld (e.g., for endangered species) |
| eco:basisOfRecord | sc:Text | ONE | Type of record (PreservedSpecimen, HumanObservation, MachineObservation, etc.) |

### Image and Observation Properties

| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:imageLicense | sc:URL | ONE | License for images in the dataset |
| eco:imageType | sc:Text | MANY | Type of images (photograph, illustration, microscopy, etc.) |
| eco:viewAngle | sc:Text | MANY | View angle of specimens in images (dorsal, ventral, lateral, etc.) |
| eco:anatomicalFeatures | sc:Text | MANY | Anatomical features visible or annotated |
| eco:phenotype | sc:Text | MANY | Observable phenotypic characteristics |

## JSON-LD Context

The recommended JSON-LD context for ecoCroissant:

```json
{
  "@context": {
    "@language": "en",
    "@vocab": "https://schema.org/",
    "sc": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "eco": "http://imageomics.org/ecoCroissant/",
    "dwc": "http://rs.tdwg.org/dwc/terms/",
    "dct": "http://purl.org/dc/terms/",
    
    "taxon": "eco:taxon",
    "taxonRank": "eco:taxonRank",
    "scientificName": "eco:scientificName",
    "taxonID": "eco:taxonID",
    "higherClassification": "eco:higherClassification",
    "vernacularName": "eco:vernacularName",
    "taxonomicStatus": "eco:taxonomicStatus",
    
    "locality": "eco:locality",
    "habitat": "eco:habitat",
    "biome": "eco:biome",
    "continent": "eco:continent",
    "coordinateUncertaintyInMeters": "eco:coordinateUncertaintyInMeters",
    "minimumElevationInMeters": "eco:minimumElevationInMeters",
    "maximumElevationInMeters": "eco:maximumElevationInMeters",
    "minimumDepthInMeters": "eco:minimumDepthInMeters",
    "maximumDepthInMeters": "eco:maximumDepthInMeters",
    
    "eventDate": "eco:eventDate",
    "eventDateStart": "eco:eventDateStart",
    "eventDateEnd": "eco:eventDateEnd",
    "seasonality": "eco:seasonality",
    "lifeStage": "eco:lifeStage",
    
    "trophicLevel": "eco:trophicLevel",
    "ecologicalRole": "eco:ecologicalRole",
    "speciesInteractions": "eco:speciesInteractions",
    "diet": "eco:diet",
    "hostOrganism": "eco:hostOrganism",
    
    "iucnStatus": "eco:iucnStatus",
    "iucnStatusSource": "eco:iucnStatusSource",
    "populationTrend": "eco:populationTrend",
    "threats": "eco:threats",
    "conservationActions": "eco:conservationActions",
    "protectedArea": "eco:protectedArea",
    
    "identificationVerificationStatus": "eco:identificationVerificationStatus",
    "identifiedBy": "eco:identifiedBy",
    "samplingProtocol": "eco:samplingProtocol",
    "dataGeneralizations": "eco:dataGeneralizations",
    "informationWithheld": "eco:informationWithheld",
    "basisOfRecord": "eco:basisOfRecord",
    
    "imageLicense": "eco:imageLicense",
    "imageType": "eco:imageType",
    "viewAngle": "eco:viewAngle",
    "anatomicalFeatures": "eco:anatomicalFeatures",
    "phenotype": "eco:phenotype"
  }
}
```

## Examples

### Example 1: Species Image Dataset (TreeOfLife-200M style)

```json
{
  "@context": {
    "@language": "en",
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "eco": "http://imageomics.org/ecoCroissant/",
    "dct": "http://purl.org/dc/terms/"
  },
  "@type": "sc:Dataset",
  "name": "TreeOfLife-200M",
  "description": "A large-scale dataset of 200 million images spanning the tree of life, designed for training species identification models.",
  "license": "https://creativecommons.org/licenses/by-nc-sa/4.0/",
  "url": "https://huggingface.co/datasets/imageomics/TreeOfLife-200M",
  "dct:conformsTo": [
    "http://mlcommons.org/croissant/1.0",
    "http://imageomics.org/ecoCroissant/1.0"
  ],
  
  "eco:taxon": ["Animalia", "Plantae", "Fungi"],
  "eco:taxonRank": "kingdom",
  "eco:higherClassification": "Life > Eukaryota > Multiple Kingdoms",
  
  "eco:habitat": ["terrestrial", "freshwater", "marine"],
  "eco:continent": ["Africa", "Antarctica", "Asia", "Europe", "North America", "Oceania", "South America"],
  
  "eco:basisOfRecord": ["HumanObservation", "PreservedSpecimen", "MachineObservation"],
  "eco:imageType": ["photograph", "museum specimen"],
  "eco:identificationVerificationStatus": "mixed - includes expert-verified and community-validated observations",
  
  "eco:samplingProtocol": "Images collected from multiple sources including iNaturalist, museum collections, and research projects",
  
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "images.tar.gz",
      "contentUrl": "https://huggingface.co/datasets/imageomics/TreeOfLife-200M/resolve/main/images.tar.gz",
      "encodingFormat": "application/gzip"
    }
  ],
  
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "species_images",
      "field": [
        {
          "@type": "cr:Field",
          "@id": "species_images/image",
          "dataType": "sc:ImageObject"
        },
        {
          "@type": "cr:Field",
          "@id": "species_images/scientific_name",
          "description": "Scientific name of the species",
          "dataType": "sc:Text"
        },
        {
          "@type": "cr:Field",
          "@id": "species_images/taxon_id",
          "description": "GBIF taxon identifier",
          "dataType": "sc:URL"
        },
        {
          "@type": "cr:Field",
          "@id": "species_images/kingdom",
          "description": "Taxonomic kingdom",
          "dataType": "sc:Text"
        }
      ]
    }
  ]
}
```

### Example 2: Butterfly Specimen Dataset

```json
{
  "@context": {
    "@language": "en",
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "eco": "http://imageomics.org/ecoCroissant/",
    "dct": "http://purl.org/dc/terms/"
  },
  "@type": "sc:Dataset",
  "name": "Heliconius Butterfly Wing Pattern Dataset",
  "description": "High-resolution images of Heliconius butterfly specimens with wing pattern annotations for studying mimicry and adaptation.",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "dct:conformsTo": [
    "http://mlcommons.org/croissant/1.0",
    "http://imageomics.org/ecoCroissant/1.0"
  ],
  
  "eco:taxon": "Heliconius",
  "eco:taxonRank": "genus",
  "eco:scientificName": "Heliconius Kluk, 1780",
  "eco:taxonID": ["https://www.gbif.org/species/1932585"],
  "eco:higherClassification": "Animalia > Arthropoda > Insecta > Lepidoptera > Nymphalidae > Heliconiinae > Heliconius",
  "eco:vernacularName": ["Longwing butterflies", "Heliconius butterflies"],
  
  "eco:habitat": ["tropical rainforest", "forest edge", "secondary forest"],
  "eco:biome": "tropical moist broadleaf forest",
  "eco:continent": ["South America", "Central America"],
  "eco:country": ["Ecuador", "Peru", "Colombia", "Panama", "Costa Rica"],
  "eco:minimumElevationInMeters": 0,
  "eco:maximumElevationInMeters": 2000,
  
  "eco:lifeStage": ["adult"],
  "eco:trophicLevel": "primary consumer",
  "eco:ecologicalRole": ["pollinator", "Müllerian mimic"],
  "eco:diet": ["pollen", "nectar"],
  "eco:hostOrganism": ["Passiflora (host plant for larvae)"],
  "eco:speciesInteractions": "Müllerian mimicry complex with other Heliconius species; larvae feed exclusively on Passiflora plants",
  
  "eco:iucnStatus": "LC",
  "eco:populationTrend": "stable",
  
  "eco:basisOfRecord": "PreservedSpecimen",
  "eco:identificationVerificationStatus": "expert-verified",
  "eco:identifiedBy": ["Museum taxonomists", "Heliconius specialists"],
  "eco:samplingProtocol": "Museum specimens imaged with standardized dorsal and ventral views",
  
  "eco:imageType": ["museum specimen photograph"],
  "eco:viewAngle": ["dorsal", "ventral"],
  "eco:anatomicalFeatures": ["forewing", "hindwing", "wing pattern"],
  "eco:phenotype": "wing color pattern"
}
```

### Example 3: Camera Trap Dataset

```json
{
  "@context": {
    "@language": "en",
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "eco": "http://imageomics.org/ecoCroissant/",
    "dct": "http://purl.org/dc/terms/"
  },
  "@type": "sc:Dataset",
  "name": "Amazon Rainforest Camera Trap Survey",
  "description": "Camera trap images of mammals from the Amazon rainforest for biodiversity monitoring and species identification.",
  "license": "https://creativecommons.org/licenses/by-nc/4.0/",
  "dct:conformsTo": [
    "http://mlcommons.org/croissant/1.0",
    "http://imageomics.org/ecoCroissant/1.0"
  ],
  
  "eco:taxon": "Mammalia",
  "eco:taxonRank": "class",
  "eco:higherClassification": "Animalia > Chordata > Mammalia",
  
  "eco:locality": "Yasuní National Park, Ecuador",
  "eco:habitat": ["lowland tropical rainforest", "terra firme forest", "várzea forest"],
  "eco:biome": "tropical moist broadleaf forest",
  "eco:continent": "South America",
  "eco:country": "Ecuador",
  "eco:coordinateUncertaintyInMeters": 10,
  "eco:minimumElevationInMeters": 200,
  "eco:maximumElevationInMeters": 400,
  
  "eco:eventDateStart": "2020-01-01",
  "eco:eventDateEnd": "2022-12-31",
  "eco:seasonality": ["wet season", "dry season"],
  
  "eco:protectedArea": "Yasuní National Park",
  "eco:threats": ["habitat fragmentation", "oil extraction", "hunting"],
  
  "eco:basisOfRecord": "MachineObservation",
  "eco:identificationVerificationStatus": "expert-verified with AI-assisted pre-classification",
  "eco:samplingProtocol": "Camera traps deployed at 1km intervals, active 24/7",
  "eco:dataGeneralizations": "Exact coordinates obscured for sensitive species locations",
  "eco:informationWithheld": "Precise locations of endangered species nesting sites withheld",
  
  "eco:imageType": ["camera trap photograph"],
  "eco:imageLicense": "https://creativecommons.org/licenses/by-nc/4.0/"
}
```

## Alignment with Darwin Core

ecoCroissant properties are designed to be compatible with [Darwin Core](https://dwc.tdwg.org/) terms where applicable. The following table shows the mapping:

| ecoCroissant Property | Darwin Core Term |
|----------------------|------------------|
| eco:taxon | dwc:scientificName |
| eco:taxonRank | dwc:taxonRank |
| eco:higherClassification | dwc:higherClassification |
| eco:vernacularName | dwc:vernacularName |
| eco:locality | dwc:locality |
| eco:habitat | dwc:habitat |
| eco:continent | dwc:continent |
| eco:country | dwc:country |
| eco:coordinateUncertaintyInMeters | dwc:coordinateUncertaintyInMeters |
| eco:eventDate | dwc:eventDate |
| eco:lifeStage | dwc:lifeStage |
| eco:basisOfRecord | dwc:basisOfRecord |
| eco:identifiedBy | dwc:identifiedBy |
| eco:samplingProtocol | dwc:samplingProtocol |

## Integration with FAIR4AI Principles

ecoCroissant supports FAIR4AI principles:

### Findable
- Standardized metadata fields enable discovery across repositories
- Links to authoritative taxonomic databases (GBIF, NCBI, EOL)
- Rich keyword and classification support

### Accessible
- Clear licensing information for data and images
- Information about data access restrictions or withheld information
- Links to data sources and repositories

### Interoperable
- JSON-LD format compatible with Croissant ecosystem
- Alignment with Darwin Core for biodiversity data exchange
- Integration with schema.org for web discoverability

### Reusable
- Detailed provenance and methodology documentation
- Data quality indicators and verification status
- Conservation context for ethical use considerations

## References

1. [Croissant: A Metadata Format for ML-Ready Datasets](https://doi.org/10.1145/3650203.3663326)
2. [Darwin Core Standard](https://dwc.tdwg.org/)
3. [GBIF Data Quality](https://www.gbif.org/data-quality-requirements)
4. [FAIR4AI Principles](https://www.nature.com/articles/s41597-022-01759-2)
5. [IUCN Red List Categories and Criteria](https://www.iucnredlist.org/resources/categories-and-criteria)
6. [Encyclopedia of Life](https://eol.org/)

## License

This specification is released under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).

## Contributors

- Imageomics Institute

## Acknowledgments

This work builds upon the [Croissant format](https://github.com/mlcommons/croissant) developed by the MLCommons Datasets Working Group.
