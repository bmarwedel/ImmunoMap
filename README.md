🧬 **ImmunoMap**

ImmunoMap is an interactive, Jupyter-based tool for predicting and visualizing immunogenicity of protein sequences. It integrates NetMHCpan and NetMHCIIpan binding predictions with similarity-based scoring against the host proteome, enabling researchers to assess MHC presentation likelihood and relative immunogenicity of each peptide segment.

🚀 **Features**

Class I & Class II MHC Binding Predictions - 
Supports human and mouse MHC alleles using NetMHCpan and NetMHCIIpan (locally installed).

Customizable Peptide Generation - 
Specify k-mer lengths, stride, and MHC class-specific parameters.

Similarity-Based Immunogenicity Scoring
Peptides are scored based on:

MHC binding affinity

BLOSUM similarity to endogenous host binders

Interactive Heatmap Visualization - 
Heatmaps of immunogenicity scores are overlaid on the input sequence, with support for:

Additive or maximum scoring mode

Per-allele or composite views

Scrollable and annotated visualizations

Proteome-Aware Filtering - 
Predicted peptides are compared to precomputed host proteome databases to filter out peptides similar to self.

📊 **Input Configuration**

Species: human, mouse

MHC Class: I, II, or Both

Allele selection with dynamic filtering based on available databases

Binding strength cutoff configuration

Customizable BLOSUM matrix

Heatmap scoring/viewing options

📁 **Host Proteome Databases**

ImmunoMap requires precomputed host binder databases for each species/allele combination. These are generated via a batch script that runs NetMHCpan/IIpan over the reference proteome and saves all peptides with binding rank.

🧪 **Example Use Case**

Paste your protein sequence (e.g., a therapeutic candidate or a mutation variant).

Select MHC class, alleles, and species.

Adjust scoring parameters and run.

Visualize the peptide heatmap to identify regions of high immunogenicity.

🛠 **Dependencies**

Python 3.10+

Jupyter Notebook

NetMHCpan and/or NetMHCIIpan (locally installed and licensed)

Biopython, pandas, matplotlib, ipywidgets

📦 **Installation**

Clone the repo and install dependencies (you must install NetMHCpan manually due to licensing):

	git clone https://github.com/bmarwedel/ImmunoMap.git

	cd ImmunoMap

	conda env create -f environment.yml

	conda activate ImmunoMap

Ensure NetMHCpan binaries are added to your PATH.

🌐 **Embedding**

ImmunoMap was designed to be used locally, but can be embedded by hosting on a cloud-based server with access to the required databases.

📅 **Roadmap**

Active development goals include:

AlphaFold-based structural overlays

Mutation suggestion engine for immunogenicity attenuation with function preservation

Broader MHC support via custom allele integration

Fully processed downloadable proteome-wide databases covering species-allele host binders with ranks

Incorporation of additional species, with priority for rats

📄 **License**

MIT License (except NetMHC tools, which require their own licenses).
