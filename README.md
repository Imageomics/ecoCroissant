# ecoCroissant

Repository for developing croissant-based biodiversity metadata schema following FAIR4AI principles.

Our goal in this repo is to first incorporate Darwin Core into the Croissant format, then start adding our particular ecological FAIR4AI terms that are needed.

See for instance [croissant-spec-1.1](https://github.com/mlcommons/croissant/blob/main/docs/croissant-spec-1.1.md) as a basis, potentially using the [RAI spec](https://github.com/mlcommons/croissant/blob/main/docs/croissant-rai-spec.md) as a model for building on top of existing schema. Note the use of schema.org as a basis, with only new terms defined. See also the [croissant.ttl](https://github.com/mlcommons/croissant/blob/main/docs/croissant.ttl).

See also, this [example JSONLD](https://doi.org/10.7717/peerj.12618).

We should also look into the Google Datasets format and indexing process (see [Dataset shema](https://schema.org/Dataset)). [Example Query](https://datasetsearch.research.google.com/search?src=0&query=tree%20of%20life&docid=L2cvMTF4ZmJyZ2s0cQ%3D%3D); for [TreeOfLife-200M](https://huggingface.co/datasets/imageomics/TreeOfLife-200M) it does captpure the DOI and the description we provide, but then the update date is "May 1, 2024", which is the GBIF snapshot we use (at least the DOI date would be logical). The correct date doesn't actually seem to be captured by Croissant either [existing-format-ex/TOL-200M-croissant](existing-format-ex/TOL-200M-croissant.jsonld). 

