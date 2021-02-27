[![Compile](https://vsrm.dev.azure.com/neuropoly/_apis/public/Release/badge/46799180-12b7-4319-b8e7-94e1d39047e7/3/12)](https://dev.azure.com/neuropoly/qMRLab/_release?view=mine&_a=releases&definitionId=3)

## Documentation pipeline

RTD documentation repository by qMRLab. Deployed by Azure pipelines.

Commits pushed to the following branches on `qMRLab/qMRLab` repository will trigger the Azure Release `documentation` pipeline:
- `doc*`
- `v2/*`
- `master`

The pipeline will generate documentation sources (using self-hosted agent for now) and push them to a branch of the same name in this (`qMRLab/documentation`) repository. 

The ReadTheDocs project is configured such that branches matching the pattern will be automatically activated. Sphinx build is done on RTD end. 

## Relevant repositories 

- `qMRLab/doc_notebooks` 
- `qMRLab/doc_images` 
