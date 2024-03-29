=================================
Using MAGPIE with GoogleColab
=================================

What is this tool?
------------------
MAGPIE is an online tool hosted on Google Colab that generates 3D visualizations for sets of protein binders interacting with one target ligand (which can be a protein or a small molecule). It also produces sequence logo-style amino acid (AA) frequency graphs. In the AA frequency graphs, the user chooses target ligand positions on the fly, and the size of each binder AA is based on the frequency that it appears in the protein complex dataset within a user-defined distance from the chosen target ligand position(s). The distance is calculated using the alpha carbon positions between protein interfaces, or all heavy atoms in the case of ligands. MAGPIE's 3D visualizer plots the entire target structure, and highlights the residues within a specified distance constraint. There are two options for coloring the interacting residues based on Amino colour and Shapely colour. If you prefer to keep the data private, or have >1000 input PDB files, it is better to clone the local version.

`A GoogleCoLab server running MAGPIE <https://colab.research.google.com/github/glasgowlab/MAGPIE/blob/GoogleColab/MAGPIE_COLAB.ipynb>`_, can be usedd to run pre-loaded example datasets or your own uploaded datasets. 

Using the GoogleColab allows users to run MAGPIE without downloading the MAGPIE package onto their local machine. The GoogleColab server provides a free cloud-based Python environment that includes all the necessary packages to run MAGPIE. The server also provides an interface to upload and run MAGPIE on your own datasets.

Required inputs:
----------------

PDB files: these should be aligned on the target ligands. Two examples are provided on GitHub, one for protein-protein interactions and one for small molecule-protein interactions
    If you choose to upload your own PDB files, you will first need to clean, standardize, and align input PDB files for seamless usage in MAGPIE

Target chain ID from PDB: the program uses the first file in the directory to upload the target ligand structure.
Protein binder chain ID from PDB: this chain identifier must be the same across all PDB files.

Target type: indicate whether the target ligand is a small molecule or a protein.

Target residue index (for protein ligands) or unique atom names (for small molecule ligands): provide the target residue indices for proteins or unique atom names for small molecules. Alternatively, you can input 'all' to consider all AAs/heavy atoms.
Usage: Please execute the cells in numerical order. If you wish to load a different dataset, start from the upload step to reload the new data.

GoogleColab Tutorial with pre-loaded datasets:
=============================================

This tutorial will guide you through using MAGPIE on the small_molecule_ligand_example dataset. This dataset has already been cleaned, standardized, and aligned on the target ligand, and can be loaded directly into MAGPIE in Step 2. 

Each cell in the Jupyter notebook should be run in order by pressing the play button on the left of the cell. The notebook is divided into sections, each of which performs a specific task.

0. Open the `GoogleColab server <https://colab.research.google.com/github/glasgowlab/MAGPIE/blob/GoogleColab/MAGPIE_COLAB.ipynb>`_.
-----------------------------------------------------------------------------------------------------------------------------------

1. Install and import required packages.
----------------------------------------

2. Upload and process data 
---------------------------
Check the box next to the small_molecule_ligand example to select this dataset. This will import the dataset from the GitHub repository and load it into MAGPIE GoogleColab.

3. Select target ligand and protein binder chains 
-------------------------------------------------
    1. Select the target ligand and protein binder chains from the dropdown menu. The target ligand chain is the chain identifier of the target ligand in the PDB file. The protein binder chain is the chain identifier of the protein binder in the PDB file. For the small molecule target example, use B for the target chain and C for the protein binder chain. 
    2. Check the is_ligand option if the target ligand is a small molecule.
    3. Provide the distance in Angstroms to graph from the target chain. 

    MAGPIE uses DBSCAN to cluster points in 3D without requiring to specify the number of desired clusters. 
    4. To run the DBSCAN feature of MAGPIE run the DBSCAN cells, choose the eps and min_samples parameters, and run the DBSCAN cells.

    eps: The maximum distance between two samples for one to be considered as in the neighborhood of the other.
    min_samples: The number of samples (or total weight) in a neighborhood for a point to be considered as a core point.
    Default is eps = 2.0, min_samples = 15'

4. Plot points in 3D viewer
---------------------------
Running this cell will open up a new window to display the plotted points in 3D.

    4.2 Plot clusters: Run this cell if you are using the DBSCAN capability

5. Select target ligand residues or heavy atoms to generate AA frequency graphs.
-------------------------------------------------------------------------------
Enter the target residue indices or heavy atom names to graph. These should be separated by commas, without spaces (e.g., N1A,N3A,N9A). Ranges are allowed when working with protein-protein interactions (e.g. 127-131,146-149).

If there are no residues within the given range, the next cell will not execute.

6. Generate AA frequency graphs
-------------------------------
Run this cell to generate the AA frequency graphs for the target residues or heavy atoms. Check the box to only display the combined AA frequency graph.

Preparing your own PDB files for use with MAGPIE GoogleColab:
=============================================================
To use your own PDB files with MAGPIE GoogleColab, you will need to clean, standardize, and align the input PDB files, by using helper scripts ``MAGPIE_input_prep.py``, ``align_protein_chain.py``, and ``align_small_molecule.py`` which can be downloaded from the `GitHub repository <https://github.com/glasgowlab/MAGPIE>`_. This requires python to be installed on your local machine. For information on how to install Python, please visit `https://www.python.org/downloads/ <https://www.python.org/downloads/>`_.

The helper script MAGPIE_input_prep.py allows the user to input files or directories with options to define target ligands and protein binders by chain, protein sequence (with percent sequence identity), ligand name (for small molecule targets), and search radius around the target. The alignment scripts align the protein-ligand complexes on the target ligand for use with MAGPIE, returning subsets of complexes for small molecule ligands as determined by user-defined all-atom RMSD. 

The coenzyme A (COA) dataset from case study #2 of `Rodriguez et al. 2023 <https://www.biorxiv.org/content/10.1101/2023.09.04.556273v2>`_ will be used in this tutorial. We used 199 structurally diverse bacterial enzymes that bind COA. We searched the PDB for structural models with refinement resolutions between 1.5 and 3 Å using its PubChem identifier code 87642. From this set of >600 structures, to reduce redundancy and noise in the dataset, we chose 199 models randomly. Using MAGPIE_input_prep.py with the small molecule target ligand name and mesh area search selection options, we removed all other chains that were not COA or the protein(s) bound/nearby to COA, including redundant protein and COA chains.

Additional examples are provided in the supplemental document of `Rodriguez et al. 2023 <https://www.biorxiv.org/content/10.1101/2023.09.04.556273v2>`_.

1. ``MAGPIE_input_prep.py``
------------------------
MAGPIE_input_prep.py is provided in the Github `GoogleCoLab branch <https://github.com/glasgowlab/MAGPIE/tree/GoogleColab>`_ to help users prepare input PDB files for MAGPIE. The helper script takes an input PDB file or directory of PDB files, an output directory, and identifying information about the protein binders and the target ligands. It outputs reformatted, renumbered PDB files in which the protein binder is on one chain and the target ligand is on another chain. The output files are found in the user-specified output directory with the suffix “_cleaned.pdb”.

.. code-block:: bash

    python ~/MAGPIE/MAGPIE_input_prep.py -i <input_directory> -o <output_directory> -L COA -M 'A,B;;COA;

2. ``align_small_molecule.py``
------------------------------
The structures are then globally aligned on COA using ``align_small_molecule.py``. All structures are exported as individual PDB files.
A threshold of 2.5 Angstroms is used here, which is the ___

.. code-block:: bash

    python ~/MAGPIE/align_small_molecule.py -c B -T 2.5 -i <input_directory> -o <output_directory> -p True

3. Import aligned PDB files into MAGPIE GoogleColab
----------------------------------------------------
Open the GoogleColab server and upload the aligned PDB files to MAGPIE GoogleColab. Navigate to the File menu located top left of the screen. Upload data into the temp directory, in the form of a compressed directory in .zip format containing the PDB input files. It is also possible to directly upload the PDB files into the temp folder, but this might take a long time depending on the number of files.