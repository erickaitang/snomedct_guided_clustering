# Ontology-Guided Clustering of SNOMED CT Disease Concepts
This notebook performs ontology-guided analysis and clustering of SNOMED CT terms using a combination of graph-based methods and node embeddings.

## Overview
- Build a directed acyclic graph (DAG) from SNOMED CT "is-a" relationships
- Subset the graph to diagnosis terms
- Generate node embeddings using Node2Vec
- Cluster these embeddings using KMeans with silhouette-guided selection of `k`
- Visualize and evaluate cluster structures via UMAP
- Annotate a diagnosis metadata file with inferred cluster IDs

## Requirements
- Python 3.8+
- Required packages: `networkx`, `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `tqdm`, `node2vec`, `umap-learn`

## External Files
- **SNOMED CT RF2 files**: Required for graph construction. Download from:
  [https://www.nlm.nih.gov/healthit/snomedct/international.html](https://www.nlm.nih.gov/healthit/snomedct/international.html)
- **Cycle removal tool** (optional): 
  [https://github.com/zhenv5/breaking_cycles_in_noisy_hierarchies](https://github.com/zhenv5/breaking_cycles_in_noisy_hierarchies)

> Note: You may point to your local RF2 folder by configuring the relevant file paths at the start of the notebook. Copyrighted SNOMED content cannot be uploaded to public repositories.

## Metadata File Format
The diagnosis metadata file must be named `Metadata.csv` and contain at least one column:

- `sct_term`: SNOMED CT terms formatted as `"CODE | DESCRIPTION"` (e.g. `123456 | Disorder of lung (disorder)`)

The notebook will automatically split this into two columns:

- `sct_code`: SNOMED CT concept ID (as a string)
- `sct_description`: Corresponding human-readable label

> Note: Make sure the codes match the concepts present in the SNOMED CT graph extracted from the RF2 files.

## Usage
This notebook is designed to be run from top to bottom in a Jupyter environment. Intermediate outputs and plots will be saved in an `Output/` directory. You may adjust clustering and embedding parameters as needed.

---
