Decoding the Rules of RNA Colocalization with Transformers
==========================================================

Overview
--------

This repository hosts the project **mRNA-Colocalization-Transformer**, a deep learning framework developed in collaboration with **Chen KOK HAO at the Genome Institute of Singapore (GIS)**. The project aims to uncover the "_Rules of Association"_ that govern how mRNAs are spatially organized within cells.

While the central dogma of biology tells us what genes are expressed, it does not reveal **where in the cell their RNA products operate**. Spatial organization is critical in groups of functionally related mRNAs often cluster to be co-regulated, co-translated, or form RNA granules.

We hypothesize that each mRNA sequence carries a **“zip code”,** which is a pattern of motifs that dictates both its subcellular localization and its preferred “neighborhood” of RNA partners. Using **transformer-based models**, we aim to predict an mRNA’s transcriptomic neighborhood directly from sequence data, thereby decoding the hidden grammar of RNA spatial organization.

Objectives
----------

*   Build a supervised deep learning model to predict **mRNA neighborhood composition** from raw sequence data.
    
*   Use **transformer architectures** (e.g., Nucleotide Transformer, RNABERT) to learn contextual dependencies and motifs across long RNA sequences.
    
*   Interpret the model through **attention maps** to discover candidate localization motifs.
    
*   Generate new **biological hypotheses** linking RNA motifs, colocalization, and functional pathways.
    

Data Sources
------------

We use **public spatial transcriptomics datasets** with single-molecule resolution, including:

*   CosMx (NanoString)
    
*   Xenium (10x Genomics)
    
*   Vizgen MERFISH
    
*   U-2 OS MERFISH dataset (Zhuang Lab)
    
*   Mouse Brain MERFISH datasets (used for early analysis sessions)
    

These datasets provide **x, y, z coordinates** for millions of mRNA molecules across cells.

Methodology
-----------

### 1\. Data Processing & Label Generation

*   Parse raw spatial transcriptomics data into structured tables (CSV/HDF5).
    
*   For each mRNA, compute its **k-nearest neighbors (k-NN)** or **radius-based neighborhood**.
    
*   Convert neighborhood composition into a **probability vector** representing the local transcriptome.
    

### 2\. Input Features

*   **Reference transcriptome sequences** (GENCODE / RefSeq).
    
*   Transform nucleotide sequences into embeddings via:
    
    *   **K-mer tokenization** (3-mer, 6-mer).
        
    *   **Secondary structure features** (via RNAfold).
        
    *   **Learned embeddings** via transformer encoders.
        

### 3\. Model Architecture

*   Transformer encoders with self-attention layers and positional encoding.
    
*   Output: a probability distribution over possible neighboring genes.
    
*   Loss functions: KL Divergence, Cross-Entropy.
    

### 4\. Evaluation

*   Compare predicted vs. true neighborhood compositions using similarity measures (cosine similarity, Jensen-Shannon divergence).
    
*   Validate biological relevance with:
    
    *   **Attention map motif discovery**.
        
    *   **Gene Ontology enrichment analysis** of predicted neighborhoods.
        

Current Progress
----------------

*   **Data exploration:** Mouse Brain MERFISH dataset analyzed to define dense/random neighborhoods
    
*   **Neighborhood modeling:** Radius-based neighborhood detection implemented; results show strong gene-specific neighbor patterns (e.g., _Cx3cl1_, _Epha7_, _Epha6_ with their nearest neighbors).
    
*   **Transformer groundwork:** Literature review of RNA-specific transformer models (RNABERT, Nucleotide Transformer) integrated into methodology.
    
*   **Notebook:** Initial Colab notebook (mRNA Colocalization.ipynb) uploaded and linked analysis data.
    
*   **Presentations:** Documented methodology, preliminary results, and future directions in two presentation decks (session1.ppt & session2.ppt).
    

Expected Outcomes
-----------------

*   Identification of novel **sequence motifs** (“zip codes”) associated with RNA colocalization.
    
*   Discovery of **functional neighborhoods** (e.g., transcripts of the glycolysis pathway clustering together).
    
*   Insights into **cell-type–specific localization rules**, such as neuron-specific clustering motifs.
    

Next Steps & Future Work
------------------------

*   Expand training on **large-scale spatial datasets** (CosMx, Vizgen).
    
*   Train and benchmark transformer models on GPU/TPU infrastructure.
    
*   Incorporate **cross-cell comparisons** to detect universal vs. cell-type–specific rules.
    
*   Use **attention heatmaps** for systematic motif discovery.
    
*   Apply **biological validation** via enrichment analyses and literature cross-checks.
    

Repository Contents
-------------------

*   **mRNA Colocalization.ipynb** – Colab notebook with preprocessing, analysis, and preliminary results
    
*   **plotly visualization:** raw MERFISH data and radius neighborhood data visualized in 3D.
    
*   **session1.ppt**– Session 1 presentation with initial MERFISH data analysis.
    
*   **session2.ppt**– Session 2 presentation focusing on transformer modeling.
    
    

Acknowledgements
----------------

This project is being carried out by **Mohit Joshi (B.Tech Biotechnology, Institute of Advanced Research)** in collaboration with **Chen Kok HAO, Genome Institute of Singapore (GIS)**.
