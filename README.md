# ecoCroissant 🥐🌿

**Croissant Extension for Biodiversity Metadata**

[![Specification](https://img.shields.io/badge/spec-v1.0-green.svg)](docs/eco-spec.md)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

## Overview

ecoCroissant makes biodiversity datasets **AI-ready** by integrating [Darwin Core](https://dwc.tdwg.org/) terms with [FAIR4AI](https://www.nature.com/articles/s41597-022-01759-2) requirements. Rather than redefining existing standards, ecoCroissant uses Darwin Core terms directly and adds AI-specific metadata for machine learning applications.

### FAIR4AI Requirements

ecoCroissant addresses the three key FAIR4AI requirements:

1. **Queryable Metadata**: Data/metadata can be queried without downloading large files (via Parquet/queryable formats)
2. **Ontology Integration**: Darwin Core terms are queryable with synonyms from GBIF, NCBI, EOL
3. **Content/Context Extraction**: Clear distinction between occurrence-based and image-based records

### AI-Ready Features

ecoCroissant ensures datasets are AI-ready by documenting:

- **Data Distribution**: Class distributions, long-tail characteristics, stratification details
- **Preprocessing Pipeline**: Standardization methods, augmentation, normalization
- **Train/Val/Test Splits**: Rationale, stratification variables, split proportions
- **Model Provenance**: For AI-generated annotations or labels
- **Streaming Support**: API endpoints and rate limits for scalable data access

## Quick Start

### Using Darwin Core with AI-Ready Metadata

ecoCroissant uses Darwin Core terms directly, adding AI-specific properties:

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
  "name": "My Biodiversity Dataset",
  "dct:conformsTo": [
    "http://mlcommons.org/croissant/1.0",
    "http://imageomics.org/ecoCroissant/1.0"
  ],
  
  "dwc:scientificName": "Lepidoptera",
  "dwc:taxonRank": "order",
  "dwc:habitat": ["tropical rainforest", "temperate forest"],
  "dwc:basisOfRecord": "PreservedSpecimen",
  
  "eco:recordType": "image-based",
  "eco:dataDistribution": "long-tailed: 5K species, 10-1000 images each",
  "eco:trainTestSplit": "80/10/10 stratified by family",
  "eco:preprocessingSteps": ["resized to 224x224", "ImageNet normalization"]
}
```

### Example Datasets

See the [examples](examples/) directory for complete examples:

- [TreeOfLife-200M](examples/treeoflife-200m.json) - AI-ready species image dataset with 200M images

## Documentation

- **[ecoCroissant Specification](docs/eco-spec.md)** - Complete specification with property definitions
- **[JSON-LD Context](schema/eco-context.jsonld)** - JSON-LD context file for ecoCroissant

## Property Categories

### Darwin Core Terms (Used Directly)

ecoCroissant uses Darwin Core terms without redefinition:

#### Taxonomic
`dwc:scientificName`, `dwc:taxonRank`, `dwc:kingdom`, `dwc:phylum`, `dwc:class`, `dwc:order`, `dwc:family`, `dwc:genus`, `dwc:taxonID`, `dwc:higherClassification`, `dwc:vernacularName`

#### Geographic
`dwc:locality`, `dwc:habitat`, `dwc:continent`, `dwc:country`, `dwc:decimalLatitude`, `dwc:decimalLongitude`, `dwc:coordinateUncertaintyInMeters`, `dwc:minimumElevationInMeters`, `dwc:maximumElevationInMeters`

#### Temporal
`dwc:eventDate`, `dwc:year`, `dwc:month`, `dwc:day`, `dwc:lifeStage`

#### Data Quality
`dwc:basisOfRecord`, `dwc:identifiedBy`, `dwc:identificationVerificationStatus`, `dwc:samplingProtocol`, `dwc:dataGeneralizations`, `dwc:informationWithheld`

### AI-Specific ecoCroissant Extensions

#### Data Distribution & Preprocessing
`eco:dataDistribution`, `eco:preprocessingSteps`, `eco:standardizationMethod`, `eco:trainTestSplit`, `eco:stratificationVariable`, `eco:dataSplitRationale`

#### Model Provenance
`eco:generatedBy`, `eco:modelConfidence`, `eco:humanVerified`, `eco:generationMethod`

#### API & Streaming
`eco:apiEndpoint`, `eco:rateLimitRequests`, `eco:rateLimitPeriod`, `eco:streamingSupported`, `eco:bulkDownloadSize`

#### Record Type Context
`eco:recordType`, `eco:occurrenceToImageRatio`, `eco:imageAnnotationType`

#### Ecological Extensions
`eco:biome`, `eco:trophicLevel`, `eco:ecologicalRole`, `eco:speciesInteractions`, `eco:diet`

#### Conservation Extensions
`eco:iucnStatus`, `eco:populationTrend`, `eco:threats`, `eco:protectedArea`

See the [full specification](docs/eco-spec.md) for complete property definitions.

## Integration with Standards

ecoCroissant is designed to integrate with established biodiversity standards:

- **[Darwin Core](https://dwc.tdwg.org/)** - Standard for biodiversity data sharing
- **[GBIF](https://www.gbif.org/)** - Global Biodiversity Information Facility
- **[IUCN Red List](https://www.iucnredlist.org/)** - Conservation status assessments
- **[Encyclopedia of Life](https://eol.org/)** - Species information aggregator

## Related Resources

- [Croissant Format](https://github.com/mlcommons/croissant) - Base ML dataset format
- [Croissant RAI Extension](https://github.com/mlcommons/croissant/blob/main/docs/croissant-rai-spec.md) - Responsible AI extension
- [TreeOfLife-200M Dataset](https://huggingface.co/datasets/imageomics/TreeOfLife-200M) - Example dataset using ecoCroissant
- [Imageomics Institute](https://imageomics.org/) - Advancing biological knowledge through images

## Contributing

We welcome contributions! Please see our contributing guidelines for more information.

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## Citation

If you use ecoCroissant in your research, please cite:

```bibtex
@misc{ecoCroissant2024,
  title={ecoCroissant: A Croissant Extension for Biodiversity Metadata},
  author={Imageomics Institute},
  year={2024},
  url={https://github.com/Imageomics/ecoCroissant}
}
```

## Acknowledgments

This work builds upon the [Croissant format](https://github.com/mlcommons/croissant) developed by the MLCommons Datasets Working Group. We thank the biodiversity informatics community for their contributions to standards like Darwin Core that inform this work.
