# CStreet Overview

CStreet is a python script (python 3) for cell trajectory construction by using k-nearest neighbors graph algorithm. It aims at time-series single-cell RNA-seq data. It is a developmental version.

# Installation

> 1. Download python scripts from github
> 2. Import the main class

```python
import sys
sys.path.append("/PATH/CStreet/src/")
from cstreet import *
```



# Quick Start

**Input file**: Time-series single cell RNA-seq data.

**Output file**: An inferenced cell trajectory.

1. Add new time-series single cell RNA-seq data.

```python
import numpy as np
import pandas as pd
# Read single cell data as DataFrame
data_t1=pd.read_table('/PATH/data_t1.txt',header=0, sep="\t",index_col=0)
data_t1=pd.read_table('/PATH/data_t2.txt',header=0, sep="\t",index_col=0)
data_t2=pd.read_table('/PATH/data_t3.txt',header=0, sep="\t",index_col=0)
data_t3=pd.read_table('/PATH/data_t4.txt',header=0, sep="\t",index_col=0)
# Create a new CStreet object
cdata=CStreetData()
# add data into CStreet object
cdata.add_new_timepoint_scdata(data_t1)
cdata.add_new_timepoint_scdata(data_t2)
cdata.add_new_timepoint_scdata(data_t3)

```

2. Customize parameters.

```python
# Cell cluster
cdata.params['cell_cluster'] = True
cdata.params['cell_cluster_pca_n'] = 10
cdata.params['cell_cluster_knn_n'] = 15
cdata.params['cell_cluster_resolution'] = 1
# Filter genes and cells
cdata.params['filter_dead_cell'] = True
cdata.params['percent_mito_cutoff'] = 0.2
cdata.params['filter_lowcell_gene'] = True
cdata.params['min_cells'] = 3
cdata.params['filter_lowgene_cells'] = True
cdata.params['min_genes'] = 200
# Data normalize
cdata.params['normalize'] = True
cdata.params['normalize_base'] = 10000
cdata.params['log_transform'] = True
# Get highly variable genes
cdata.params['highly_variable_genes'] = False
# Set PCA and kNN
cdata.params['inner_graph_pca_n'] = 10
cdata.params['inner_graph_knn_n'] = 15
cdata.params['link_graph_pca_n'] = 10
cdata.params['link_graph_knn_n'] = 15
# Draw trajectory
cdata.params['max_outgoing'] = 10
cdata.params['min_score'] = 0.1
```

3. Run CStreet

```python
cdata.run_cstreet()
```



# Result

**An example of inferenced cell trajectory**:

![results.png](https://github.com/yw-Hua/MarkdownPicture/blob/master/CStreet/results.png?raw=true)
