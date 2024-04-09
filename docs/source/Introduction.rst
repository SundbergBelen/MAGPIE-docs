==================
What is this MAGPIE?
==================
MAGPIE is an online tool that generates 3D visualizations for sets of protein binders interacting with one target ligand (which can be a protein or a small molecule). It also produces sequence logo-style amino acid (AA) frequency graphs. In the AA frequency graphs, the user chooses target ligand positions on the fly, and the size of each binder AA is based on the frequency that it appears in the protein complex dataset within a user-defined distance from the chosen target ligand position(s). The distance is calculated using the alpha carbon positions between protein interfaces, or all heavy atoms in the case of ligands. MAGPIE's 3D visualizer plots the entire target structure, and highlights the residues within a specified distance constraint. There are two options for coloring the interacting residues based on `Amino colour <https://acces.ens-lyon.fr/biotic/rastop/help/colour.htm#aminocolours>`_ and `Shapely colour <https://acces.ens-lyon.fr/biotic/rastop/help/colour.htm#shapelycolours>`_. 

MAGPIE can be used in three different ways: 
--------------------------------------------

1. As a pre-installed Jupyter Notebook on the GoogleColab server 

2. Via local installation (This is the most powerful and flexible version of MAGPIE that is compatible with multithreading and includes the PyRosetta-dependent energy calculation feature.If you prefer to keep the data private, or have >1000 input PDB files, it is better to clone the local version.)

3. As a GUI

The `MAGPIE GoogleColab server <https://colab.research.google.com/github/glasgowlab/MAGPIE/blob/GoogleColab/MAGPIE_COLAB.ipynb>`_ provides a free cloud-based Python environment that includes all the necessary packages to run MAGPIE without downloading the MAGPIE package onto their local machine. The GoogleColab server can be used to run pre-loaded example datasets and also provides an interface for users to upload and run their own datasets.

Alternatively, the Local-Version of MAGPIE can be downloaded from github and run on a local machine. This version of MAGPIE is recommended for users who wish to keep their data private, or have >1000 input PDB files. The Local-Version of MAGPIE requires the user to have Python 3 installed on their machine, as well as the following Python packages: Numpy (1.18.5), Pandas (1.3.4), Matplotlib (3.4.3), Glob (0.7), Plotly (5.9.0), and Spicy (1.7.1). The Local-Version of MAGPIE can be downloaded from the `MAGPIE Github repository <https://github.com/glasgowlab/MAGPIE/tree/local-version>`_.

Detailed instructions on how to use the GoogleColab or the Local-Version of MAGPIE are provided in this documentation.