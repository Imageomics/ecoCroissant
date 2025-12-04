# ecoCroissant 🥐🌿

**Croissant Extension for Biodiversity Metadata**

[![Specification](https://img.shields.io/badge/spec-v1.0-green.svg)](docs/eco-spec.md)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

## Overview

ecoCroissant is an extension to the [Croissant format](https://github.com/mlcommons/croissant) designed to capture ecologically-relevant information from biodiversity datasets. It follows [FAIR4AI principles](https://www.nature.com/articles/s41597-022-01759-2) to ensure datasets are Findable, Accessible, Interoperable, and Reusable for AI/ML applications in ecological and biodiversity research.

## Why ecoCroissant?

The standard Croissant format provides excellent support for ML-ready datasets, but biodiversity datasets have unique characteristics that require additional metadata:

- **Taxonomic Information**: Species identification, taxonomic hierarchies, and nomenclature
- **Geographic Context**: Collection locations, habitats, elevation, and protected areas  
- **Temporal Ecology**: Phenology, seasonality, and collection timelines
- **Ecological Relationships**: Trophic levels, species interactions, and ecological roles
- **Conservation Status**: IUCN categories, population trends, and threats
- **Data Quality**: Identification confidence, georeferencing accuracy, and sampling methods

## Quick Start

### Using ecoCroissant Properties

Add the ecoCroissant context to your Croissant metadata:

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
  "name": "My Biodiversity Dataset",
  "dct:conformsTo": [
    "http://mlcommons.org/croissant/1.0",
    "http://imageomics.org/ecoCroissant/1.0"
  ],
  
  "eco:taxon": "Lepidoptera",
  "eco:taxonRank": "order",
  "eco:habitat": ["tropical rainforest", "temperate forest"],
  "eco:iucnStatus": "LC",
  "eco:basisOfRecord": "PreservedSpecimen"
}
```

### Example Datasets

See the [examples](examples/) directory for complete examples:

- [TreeOfLife-200M](examples/treeoflife-200m.json) - Large-scale species image dataset

## Documentation

- **[ecoCroissant Specification](docs/eco-spec.md)** - Complete specification with property definitions
- **[JSON-LD Context](schema/eco-context.jsonld)** - JSON-LD context file for ecoCroissant

## Property Categories

### Taxonomic Properties
| Property | Description |
|----------|-------------|
| `eco:taxon` | Taxonomic name(s) of organisms |
| `eco:taxonRank` | Taxonomic rank (species, genus, family, etc.) |
| `eco:scientificName` | Full scientific name with authorship |
| `eco:taxonID` | Links to GBIF, NCBI, or other databases |
| `eco:higherClassification` | Full taxonomic hierarchy |

### Geographic Properties
| Property | Description |
|----------|-------------|
| `eco:habitat` | Habitat type(s) |
| `eco:biome` | Major biome classification |
| `eco:locality` | Location description |
| `eco:protectedArea` | Protected areas where species occurs |

### Conservation Properties
| Property | Description |
|----------|-------------|
| `eco:iucnStatus` | IUCN Red List category |
| `eco:populationTrend` | Population trend direction |
| `eco:threats` | Known threats to species |

### Data Quality Properties
| Property | Description |
|----------|-------------|
| `eco:basisOfRecord` | Type of record (specimen, observation, etc.) |
| `eco:identificationVerificationStatus` | Verification level |
| `eco:samplingProtocol` | Data collection method |

See the [full specification](docs/eco-spec.md) for all available properties.

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
