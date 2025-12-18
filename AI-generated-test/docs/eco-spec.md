# ecoCroissant Specification

## Croissant Extension for Biodiversity Metadata

Version 1.0

<http://imageomics.org/ecoCroissant/1.0>

## Introduction

ecoCroissant is an extension to the [Croissant format](http://mlcommons.org/croissant/1.0) designed to make biodiversity datasets **AI-ready** by integrating Darwin Core terms with FAIR4AI-specific requirements. Rather than redefining existing biodiversity standards, ecoCroissant builds upon [Darwin Core](https://dwc.tdwg.org/) terms and enhances them with AI-specific metadata needed for machine learning applications.

### FAIR4AI Requirements

ecoCroissant specifically addresses FAIR4AI requirements:

1. **Queryable Metadata**: Data and metadata can be queried without downloading large files or specialized file types
2. **Ontology Integration**: Darwin Core terms are directly integrated, queryable with synonyms from other biodiversity ontologies (GBIF, NCBI, EOL)
3. **Content/Context Extraction**: Clear distinction between occurrence-based and image-based data records

### AI-Ready Data Requirements

ecoCroissant ensures datasets are **AI-ready** by including:

- **Distribution Information**: Data splits, stratification details, and class distributions in usable form
- **Preprocessing Documentation**: Information about whether data has been processed or standardized and how
- **Model Provenance**: For AI-generated annotations or classifications
- **Rate Limiting**: Server profiling information for streaming data from sources

### Extension Scope

ecoCroissant extends Croissant by:

- **Direct Darwin Core Integration**: Using Darwin Core terms natively rather than redefining them
- **AI-Specific Metadata**: Adding properties for model provenance, data splits, and preprocessing pipelines
- **Ecological Context**: Properties for ecological relationships and conservation status not in Darwin Core
- **Image-Specific Metadata**: Properties for anatomical features, view angles, and image types relevant to biodiversity ML

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

## Properties

ecoCroissant uses Darwin Core terms directly where applicable and adds new properties only when needed for AI-specific requirements or ecological concepts not covered by Darwin Core.

### Darwin Core Properties (Used Directly)

The following Darwin Core terms are used directly without redefinition:

#### Taxonomic Terms
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| dwc:scientificName | sc:Text | ONE | The full scientific name including authorship |
| dwc:taxonRank | sc:Text | ONE | The taxonomic rank (e.g., species, genus, family) |
| dwc:kingdom | sc:Text | ONE | Taxonomic kingdom |
| dwc:phylum | sc:Text | ONE | Taxonomic phylum |
| dwc:class | sc:Text | ONE | Taxonomic class |
| dwc:order | sc:Text | ONE | Taxonomic order |
| dwc:family | sc:Text | ONE | Taxonomic family |
| dwc:genus | sc:Text | ONE | Taxonomic genus |
| dwc:higherClassification | sc:Text | ONE | Full taxonomic hierarchy |
| dwc:vernacularName | sc:Text | MANY | Common name(s) in various languages |
| dwc:taxonomicStatus | sc:Text | ONE | Status of the taxon name (accepted, synonym, etc.) |
| dwc:taxonID | sc:URL | MANY | Identifier from taxonomic databases (GBIF, NCBI, etc.) |

#### Geographic Terms
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| dwc:locality | sc:Text | ONE | Description of the location |
| dwc:habitat | sc:Text | MANY | Habitat type(s) where organisms occur |
| dwc:continent | sc:Text | ONE | Continent of occurrence |
| dwc:country | sc:Text | MANY | Country/countries of occurrence |
| dwc:coordinateUncertaintyInMeters | sc:Number | ONE | Uncertainty radius for coordinates |
| dwc:minimumElevationInMeters | sc:Number | ONE | Minimum elevation of occurrences |
| dwc:maximumElevationInMeters | sc:Number | ONE | Maximum elevation of occurrences |
| dwc:minimumDepthInMeters | sc:Number | ONE | Minimum depth (for aquatic organisms) |
| dwc:maximumDepthInMeters | sc:Number | ONE | Maximum depth (for aquatic organisms) |
| dwc:decimalLatitude | sc:Float | ONE | Latitude in decimal degrees |
| dwc:decimalLongitude | sc:Float | ONE | Longitude in decimal degrees |
| dwc:geodeticDatum | sc:Text | ONE | Spatial reference system (e.g., WGS84) |

#### Temporal Terms
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| dwc:eventDate | sc:Date or sc:DateTime | MANY | Date(s) when data was collected |
| dwc:year | sc:Integer | ONE | Year of collection |
| dwc:month | sc:Integer | ONE | Month of collection |
| dwc:day | sc:Integer | ONE | Day of collection |
| dwc:lifeStage | sc:Text | MANY | Life stage(s) represented (egg, larva, adult, etc.) |

#### Data Quality Terms
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| dwc:identificationVerificationStatus | sc:Text | ONE | Verification level of taxonomic identifications |
| dwc:identifiedBy | sc:Text | MANY | Who identified the specimens/observations |
| dwc:samplingProtocol | sc:Text | ONE | Method used to collect data |
| dwc:dataGeneralizations | sc:Text | ONE | Any data generalizations applied (e.g., coordinate obscuring) |
| dwc:informationWithheld | sc:Text | ONE | Information intentionally withheld (e.g., for endangered species) |
| dwc:basisOfRecord | sc:Text | ONE | Type of record (PreservedSpecimen, HumanObservation, MachineObservation, etc.) |
| dwc:occurrenceStatus | sc:Text | ONE | Whether organism was present or absent |

### AI-Specific Properties (ecoCroissant Extensions)

These properties are ecoCroissant additions for AI-ready data requirements:

#### Data Distribution and Preprocessing
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:dataDistribution | sc:Text | ONE | Description of class distribution (e.g., "long-tailed", "balanced", stratification details) |
| eco:preprocessingSteps | sc:Text | MANY | List of preprocessing steps applied (e.g., "resized to 224x224", "normalized to [-1,1]") |
| eco:standardizationMethod | sc:Text | ONE | Method used for data standardization if applicable |
| eco:trainTestSplit | sc:Text | ONE | Description of train/test/validation splits with proportions |
| eco:stratificationVariable | sc:Text | MANY | Variables used for stratification (e.g., "taxonomic family", "geographic region") |
| eco:dataSplitRationale | sc:Text | ONE | Rationale for data splitting strategy |

#### Model Provenance for AI-Generated Data
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:generatedBy | sc:Text | ONE | Name/version of model that generated annotations or classifications |
| eco:modelConfidence | sc:Float | ONE | Confidence score for AI-generated labels (0-1) |
| eco:humanVerified | sc:Boolean | ONE | Whether AI-generated data has been human-verified |
| eco:generationMethod | sc:Text | ONE | Method used for generation (e.g., "automated classification", "bounding box detection") |

#### API and Streaming Information
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:apiEndpoint | sc:URL | ONE | API endpoint for streaming data access |
| eco:rateLimitRequests | sc:Integer | ONE | Maximum requests per time period |
| eco:rateLimitPeriod | sc:Text | ONE | Time period for rate limit (e.g., "per minute", "per hour") |
| eco:streamingSupported | sc:Boolean | ONE | Whether data can be streamed rather than downloaded |
| eco:bulkDownloadSize | sc:Text | ONE | Approximate size of full dataset download |

#### Record Type Context (FAIR4AI Requirement)
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:recordType | sc:Text | ONE | Type of data record: "occurrence-based" or "image-based" or "mixed" |
| eco:occurrenceToImageRatio | sc:Float | ONE | Ratio of occurrence records to images (relevant for mixed datasets) |
| eco:imageAnnotationType | sc:Text | MANY | Type of image annotations (e.g., "bounding box", "segmentation", "whole image classification") |

#### Ecological Extensions (Not in Darwin Core)
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:biome | sc:Text | ONE | Major biome classification |
| eco:trophicLevel | sc:Text | ONE | Position in food chain (producer, primary consumer, etc.) |
| eco:ecologicalRole | sc:Text | MANY | Ecological function (pollinator, predator, decomposer, etc.) |
| eco:speciesInteractions | sc:Text | MANY | Description of species interactions in the dataset |
| eco:diet | sc:Text | MANY | Diet composition for animals |

#### Conservation Extensions
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:iucnStatus | sc:Text | ONE | IUCN Red List category (LC, NT, VU, EN, CR, EW, EX) |
| eco:iucnStatusSource | sc:URL | ONE | Link to IUCN assessment |
| eco:populationTrend | sc:Text | ONE | Population trend (increasing, stable, decreasing, unknown) |
| eco:threats | sc:Text | MANY | Known threats to the species |
| eco:conservationActions | sc:Text | MANY | Conservation actions in place or recommended |
| eco:protectedArea | sc:Text | MANY | Protected areas where species occurs |

#### Image-Specific Extensions
| Property | Expected Type | Cardinality | Description |
|----------|---------------|-------------|-------------|
| eco:imageLicense | sc:URL | ONE | License for images in the dataset |
| eco:imageType | sc:Text | MANY | Type of images (photograph, illustration, microscopy, etc.) |
| eco:viewAngle | sc:Text | MANY | View angle of specimens in images (dorsal, ventral, lateral, etc.) |
| eco:anatomicalFeatures | sc:Text | MANY | Anatomical features visible or annotated |
| eco:phenotype | sc:Text | MANY | Observable phenotypic characteristics |
| eco:imageResolution | sc:Text | ONE | Resolution of images (e.g., "1024x1024", "variable") |
| eco:imageFormat | sc:Text | MANY | Image file formats (e.g., "JPEG", "PNG", "TIFF") |

## JSON-LD Context

The recommended JSON-LD context for ecoCroissant uses Darwin Core terms directly:

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
    
    "scientificName": "dwc:scientificName",
    "taxonRank": "dwc:taxonRank",
    "kingdom": "dwc:kingdom",
    "phylum": "dwc:phylum",
    "class": "dwc:class",
    "order": "dwc:order",
    "family": "dwc:family",
    "genus": "dwc:genus",
    "taxonID": "dwc:taxonID",
    "higherClassification": "dwc:higherClassification",
    "vernacularName": "dwc:vernacularName",
    "taxonomicStatus": "dwc:taxonomicStatus",
    
    "locality": "dwc:locality",
    "habitat": "dwc:habitat",
    "continent": "dwc:continent",
    "country": "dwc:country",
    "decimalLatitude": "dwc:decimalLatitude",
    "decimalLongitude": "dwc:decimalLongitude",
    "coordinateUncertaintyInMeters": "dwc:coordinateUncertaintyInMeters",
    "minimumElevationInMeters": "dwc:minimumElevationInMeters",
    "maximumElevationInMeters": "dwc:maximumElevationInMeters",
    "minimumDepthInMeters": "dwc:minimumDepthInMeters",
    "maximumDepthInMeters": "dwc:maximumDepthInMeters",
    "geodeticDatum": "dwc:geodeticDatum",
    
    "eventDate": "dwc:eventDate",
    "year": "dwc:year",
    "month": "dwc:month",
    "day": "dwc:day",
    "lifeStage": "dwc:lifeStage",
    
    "identificationVerificationStatus": "dwc:identificationVerificationStatus",
    "identifiedBy": "dwc:identifiedBy",
    "samplingProtocol": "dwc:samplingProtocol",
    "dataGeneralizations": "dwc:dataGeneralizations",
    "informationWithheld": "dwc:informationWithheld",
    "basisOfRecord": "dwc:basisOfRecord",
    "occurrenceStatus": "dwc:occurrenceStatus",
    
    "dataDistribution": "eco:dataDistribution",
    "preprocessingSteps": "eco:preprocessingSteps",
    "standardizationMethod": "eco:standardizationMethod",
    "trainTestSplit": "eco:trainTestSplit",
    "stratificationVariable": "eco:stratificationVariable",
    "dataSplitRationale": "eco:dataSplitRationale",
    
    "generatedBy": "eco:generatedBy",
    "modelConfidence": "eco:modelConfidence",
    "humanVerified": "eco:humanVerified",
    "generationMethod": "eco:generationMethod",
    
    "apiEndpoint": "eco:apiEndpoint",
    "rateLimitRequests": "eco:rateLimitRequests",
    "rateLimitPeriod": "eco:rateLimitPeriod",
    "streamingSupported": "eco:streamingSupported",
    "bulkDownloadSize": "eco:bulkDownloadSize",
    
    "recordType": "eco:recordType",
    "occurrenceToImageRatio": "eco:occurrenceToImageRatio",
    "imageAnnotationType": "eco:imageAnnotationType",
    
    "biome": "eco:biome",
    "trophicLevel": "eco:trophicLevel",
    "ecologicalRole": "eco:ecologicalRole",
    "speciesInteractions": "eco:speciesInteractions",
    "diet": "eco:diet",
    
    "iucnStatus": "eco:iucnStatus",
    "iucnStatusSource": "eco:iucnStatusSource",
    "populationTrend": "eco:populationTrend",
    "threats": "eco:threats",
    "conservationActions": "eco:conservationActions",
    "protectedArea": "eco:protectedArea",
    
    "imageLicense": "eco:imageLicense",
    "imageType": "eco:imageType",
    "viewAngle": "eco:viewAngle",
    "anatomicalFeatures": "eco:anatomicalFeatures",
    "phenotype": "eco:phenotype",
    "imageResolution": "eco:imageResolution",
    "imageFormat": "eco:imageFormat",
    
    "column": "cr:column",
    "conformsTo": "dct:conformsTo",
    "data": {
      "@id": "cr:data",
      "@type": "@json"
    },
    "dataType": {
      "@id": "cr:dataType",
      "@type": "@vocab"
    },
    "examples": {
      "@id": "cr:examples",
      "@type": "@json"
    },
    "extract": "cr:extract",
    "field": "cr:field",
    "fileProperty": "cr:fileProperty",
    "fileObject": "cr:fileObject",
    "fileSet": "cr:fileSet",
    "format": "cr:format",
    "includes": "cr:includes",
    "isLiveDataset": "cr:isLiveDataset",
    "jsonPath": "cr:jsonPath",
    "key": "cr:key",
    "md5": "cr:md5",
    "parentField": "cr:parentField",
    "path": "cr:path",
    "recordSet": "cr:recordSet",
    "references": "cr:references",
    "regex": "cr:regex",
    "repeated": "cr:repeated",
    "replace": "cr:replace",
    "separator": "cr:separator",
    "source": "cr:source",
    "subField": "cr:subField",
    "transform": "cr:transform"
  }
}
```

## Examples

### Example 1: AI-Ready Species Image Dataset (TreeOfLife-200M style)

```json
{
  "@context": {
    "@language": "en",
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "eco": "http://imageomics.org/ecoCroissant/",
    "dwc": "http://rs.tdwg.org/dwc/terms/",
    "dct": "http://purl.org/dc/terms/"
  },
  "@type": "sc:Dataset",
  "name": "TreeOfLife-200M",
  "description": "AI-ready dataset of 200M images spanning the tree of life with stratified splits for species identification. Images from iNaturalist Research Grade observations.",
  "license": "https://creativecommons.org/licenses/by-nc-sa/4.0/",
  "url": "https://huggingface.co/datasets/imageomics/TreeOfLife-200M",
  "dct:conformsTo": [
    "http://mlcommons.org/croissant/1.0",
    "http://imageomics.org/ecoCroissant/1.0"
  ],
  
  "dwc:basisOfRecord": ["HumanObservation"],
  "dwc:identificationVerificationStatus": "Research Grade (2/3+ community agreement)",
  "dwc:samplingProtocol": "Community science observations via iNaturalist platform",
  "dwc:dataGeneralizations": "Coordinates obscured for sensitive species per observer privacy settings",
  
  "eco:recordType": "image-based",
  "eco:dataDistribution": "long-tailed: 500K species with 1-10,000 images each, stratified by taxonomic family",
  "eco:preprocessingSteps": ["resized to 224x224", "normalized to ImageNet stats", "augmented with random crops and flips"],
  "eco:standardizationMethod": "ImageNet normalization (mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])",
  "eco:trainTestSplit": "80% train, 10% validation, 10% test - stratified by species",
  "eco:stratificationVariable": ["dwc:family", "dwc:genus"],
  "eco:dataSplitRationale": "Stratified to ensure representation across taxonomic groups; temporal split avoided due to seasonal biases",
  
  "eco:apiEndpoint": "https://huggingface.co/api/datasets/imageomics/TreeOfLife-200M",
  "eco:streamingSupported": true,
  "eco:bulkDownloadSize": "~15TB uncompressed",
  "eco:rateLimitRequests": 1000,
  "eco:rateLimitPeriod": "per hour",
  
  "eco:imageType": ["photograph"],
  "eco:imageResolution": "variable - minimum 224x224, maximum 4096x4096",
  "eco:imageFormat": ["JPEG"],
  "eco:imageLicense": "https://creativecommons.org/licenses/by-nc/4.0/",
  
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "metadata.parquet",
      "name": "metadata.parquet",
      "description": "Queryable metadata without downloading images",
      "contentUrl": "https://huggingface.co/datasets/imageomics/TreeOfLife-200M/resolve/main/metadata.parquet",
      "encodingFormat": "application/x-parquet"
    }
  ],
  
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "species_images",
      "field": [
        {
          "@type": "cr:Field",
          "@id": "species_images/image_id",
          "dataType": "sc:Text"
        },
        {
          "@type": "cr:Field",
          "@id": "species_images/scientificName",
          "description": "Darwin Core scientific name",
          "dataType": "dwc:scientificName"
        },
        {
          "@type": "cr:Field",
          "@id": "species_images/taxonID",
          "description": "iNaturalist taxon identifier linking to GBIF",
          "dataType": "dwc:taxonID"
        },
        {
          "@type": "cr:Field",
          "@id": "species_images/kingdom",
          "dataType": "dwc:kingdom"
        },
        {
          "@type": "cr:Field",
          "@id": "species_images/family",
          "dataType": "dwc:family"
        },
        {
          "@type": "cr:Field",
          "@id": "species_images/split",
          "description": "train/val/test split assignment",
          "dataType": "sc:Text"
        }
      ]
    }
  ]
}
```

### Example 2: Butterfly Specimen Dataset with AI-Generated Annotations

```json
{
  "@context": {
    "@language": "en",
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "eco": "http://imageomics.org/ecoCroissant/",
    "dwc": "http://rs.tdwg.org/dwc/terms/",
    "dct": "http://purl.org/dc/terms/"
  },
  "@type": "sc:Dataset",
  "name": "Heliconius Butterfly Wing Pattern Dataset",
  "description": "AI-ready dataset of museum specimens with standardized imaging and AI-assisted wing pattern segmentations.",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "dct:conformsTo": [
    "http://mlcommons.org/croissant/1.0",
    "http://imageomics.org/ecoCroissant/1.0"
  ],
  
  "dwc:scientificName": "Heliconius Kluk, 1780",
  "dwc:taxonRank": "genus",
  "dwc:taxonID": "https://www.gbif.org/species/1932585",
  "dwc:higherClassification": "Animalia > Arthropoda > Insecta > Lepidoptera > Nymphalidae > Heliconiinae > Heliconius",
  "dwc:vernacularName": ["Longwing butterflies"],
  "dwc:kingdom": "Animalia",
  "dwc:class": "Insecta",
  "dwc:order": "Lepidoptera",
  "dwc:family": "Nymphalidae",
  "dwc:genus": "Heliconius",
  
  "dwc:habitat": ["tropical rainforest", "forest edge", "secondary forest"],
  "dwc:continent": ["South America", "Central America"],
  "dwc:country": ["Ecuador", "Peru", "Colombia", "Panama", "Costa Rica"],
  "dwc:minimumElevationInMeters": 0,
  "dwc:maximumElevationInMeters": 2000,
  
  "dwc:lifeStage": ["adult"],
  "dwc:basisOfRecord": "PreservedSpecimen",
  "dwc:identificationVerificationStatus": "expert-verified",
  "dwc:identifiedBy": ["Museum taxonomists", "Heliconius specialists"],
  "dwc:samplingProtocol": "Museum specimens imaged with standardized dorsal and ventral views at 300 DPI",
  
  "eco:biome": "tropical moist broadleaf forest",
  "eco:trophicLevel": "primary consumer",
  "eco:ecologicalRole": ["pollinator", "Müllerian mimic"],
  "eco:diet": ["pollen", "nectar"],
  "eco:speciesInteractions": "Müllerian mimicry complex; larvae on Passiflora",
  
  "eco:iucnStatus": "LC",
  "eco:populationTrend": "stable",
  
  "eco:recordType": "image-based",
  "eco:preprocessingSteps": ["white background removal", "standardized to 1024x1024", "color-corrected"],
  "eco:imageType": ["museum specimen photograph"],
  "eco:imageResolution": "1024x1024",
  "eco:imageFormat": ["TIFF", "JPEG"],
  "eco:viewAngle": ["dorsal", "ventral"],
  "eco:anatomicalFeatures": ["forewing", "hindwing", "wing pattern"],
  "eco:phenotype": "wing color pattern",
  "eco:imageAnnotationType": ["segmentation"],
  
  "eco:generatedBy": "Mask R-CNN v2.1 trained on 5K hand-annotated specimens",
  "eco:modelConfidence": 0.92,
  "eco:humanVerified": true,
  "eco:generationMethod": "automated wing boundary segmentation with manual correction"
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

## Darwin Core Integration

ecoCroissant uses Darwin Core terms directly as part of its vocabulary. There is no separate "ecoCroissant version" of Darwin Core terms - the standard Darwin Core terms are used natively through the `dwc:` namespace.

### Direct Darwin Core Usage

All Darwin Core terms are available for use in ecoCroissant datasets. The most commonly used terms include:

- **Taxonomic**: `dwc:scientificName`, `dwc:taxonRank`, `dwc:kingdom`, `dwc:phylum`, `dwc:class`, `dwc:order`, `dwc:family`, `dwc:genus`, `dwc:higherClassification`, `dwc:taxonID`, `dwc:vernacularName`, `dwc:taxonomicStatus`
- **Geographic**: `dwc:locality`, `dwc:habitat`, `dwc:continent`, `dwc:country`, `dwc:decimalLatitude`, `dwc:decimalLongitude`, `dwc:coordinateUncertaintyInMeters`, `dwc:geodeticDatum`, elevation and depth terms
- **Temporal**: `dwc:eventDate`, `dwc:year`, `dwc:month`, `dwc:day`
- **Data Quality**: `dwc:basisOfRecord`, `dwc:identifiedBy`, `dwc:identificationVerificationStatus`, `dwc:samplingProtocol`, `dwc:dataGeneralizations`, `dwc:informationWithheld`

### Queryability with Ontology Synonyms

Darwin Core terms in ecoCroissant datasets can be queried using synonyms from other biodiversity ontologies:

- **GBIF Backbone Taxonomy**: `dwc:taxonID` can link to GBIF species pages
- **NCBI Taxonomy**: Cross-reference via taxon identifiers
- **Encyclopedia of Life (EOL)**: Link species concepts across systems
- **Integrated Taxonomic Information System (ITIS)**: Standard taxonomic references

This satisfies the FAIR4AI requirement that "ontology used can be queried with synonyms from other ontologies."

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
