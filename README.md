# Ontology-Guided Clustering of SNOMED CT Disease Concepts
This notebook performs ontology-guided analysis and clustering of SNOMED CT terms using a combination of graph-based methods and node embeddings.

## Overview
- Builds a directed acyclic graph (DAG) from SNOMED CT "is-a" relationships
- Subsets the graph to diagnosis terms
- Generates node embeddings using Node2Vec
- Clusters the embeddings using KMeans, with silhouette-guided selection of `k`
- Visualizes and evaluates cluster structures using UMAP
- Annotates a diagnosis metadata file with inferred cluster IDs

## Requirements
- Python 3.8+
- Required packages: `networkx`, `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `tqdm`, `node2vec`, `umap-learn`

## External Files

### SNOMED CT RF2 files  
Download from:  
👉 [https://www.nlm.nih.gov/healthit/snomedct/international.html](https://www.nlm.nih.gov/healthit/snomedct/international.html)

> **Note**: SNOMED CT content is licensed and cannot be uploaded to public repositories. Download the RF2 files manually and set your file paths at the start of the notebook.

### Cycle removal tool  
Clone from:  
👉 [https://github.com/zhenv5/breaking_cycles_in_noisy_hierarchies](https://github.com/zhenv5/breaking_cycles_in_noisy_hierarchies)

> **Note**: Clone into a subfolder named `remove_cyclic_edges`.

## Metadata File Format
The diagnosis metadata file must be named `Metadata.csv` and contain a column:

- `sct_term`: SNOMED CT terms formatted as `"CODE | DESCRIPTION"` (e.g., `123456 | Disorder of lung (disorder)`)

The notebook automatically splits this into:

- `sct_code`: SNOMED CT concept ID (string)
- `sct_description`: Human-readable label

> **Important**: Ensure that `sct_code` entries match concepts present in the SNOMED CT graph derived from the RF2 files.

## Usage
Run the notebook top to bottom in a Jupyter environment. Outputs (e.g., embeddings, plots, cluster assignments) will be saved in an `Output/` directory. You can customize Node2Vec and clustering parameters near the top of the script.

---

