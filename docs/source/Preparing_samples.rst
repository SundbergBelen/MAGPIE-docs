============================================
Preparing your own dataset for use in MAGPIE
============================================

To use your own PDB files with MAGPIE GoogleColab or Local-Version, you will need to clean, standardize, and align the input PDB files, by using helper scripts ``MAGPIE_input_prep.py``, ``align_protein_chain.py``, and ``align_small_molecule.py`` which can be downloaded from the `GitHub repository <https://github.com/glasgowlab/MAGPIE>`_ if you are using the GoogleColab version of MAGPIE. If you have downloaded the Local-Version of MAGPIE, these scripts are included in the downloaded repository. Use of the MAGPIE helper scripts requires python to be installed on your local machine. For information on how to install Python, please visit `https://www.python.org/downloads/ <https://www.python.org/downloads/>`_.

Description of helper scripts
------------------------------
``MAGPIE_input_prep.py`` allows the user to input files or directories with options to define target ligands and protein binders by chain, protein sequence (with percent sequence identity), ligand name (for small molecule targets), and search radius around the target. The alignment scripts align the protein-ligand complexes on the target ligand for use with MAGPIE, returning subsets of complexes for small molecule ligands as determined by user-defined all-atom RMSD. 

``align_protein_chain.py`` is an alignment script for structural models with target ligands that are proteins. This alignment script will align the protein binders on the target protein chain for use with MAGPIE, returning subsets of complexes for protein ligands as determined by user-defined all-atom RMSD. **CHECK THIS**

``align_small_molecule.py`` is an alignment script for structural models with target ligands that are small molecules. This alignment script will align the protein-ligand complexes on the target ligand for use with MAGPIE, returning subsets of complexes for small molecule ligands as determined by user-defined all-atom RMSD.

Tutorial
---------
**1. Run** ``MAGPIE_input_prep.py``

 This helper script takes an input PDB file or directory of PDB files, an output directory, and identifying information about the protein binders and the target ligands. It outputs reformatted, renumbered PDB files in which the protein binder is on one chain and the target ligand is on another chain. The output files are found in the user-specified output directory with the suffix “_cleaned.pdb”.

.. code-block:: bash

    python ~/MAGPIE/MAGPIE_input_prep.py -i <input_directory> -o <output_directory> -L COA -M 'A,B;;COA;'

**2. Run align Protein Chain or Align Small Molecule scripts** 

**A.**  ``align_protein_chain.py``

The protein binders are aligned on the target ligand using ``align_protein_chain.py``. All structures are exported as individual PDB files. An RMSD threshold of 2.5 Angstroms is used here.

NEED EXAMPLE CODE HERE

**B.** ``align_small_molecule.py``

The structures are then globally aligned on COA using ``align_small_molecule.py``. All structures are exported as individual PDB files.
An RMSD threshold of 2.5 Angstroms is used here.

.. code-block:: bash

    python ~/MAGPIE/align_small_molecule.py -c B -T 2.5 -i <input_directory> -o <output_directory> -p True

**3. Import aligned PDB files into MAGPIE GoogleColab**

**A. GoogleColab Version**

3.1 Open the GoogleColab server. 

3.2 Navigate to the File menu located top left of the screen. 

3.3 Upload data into the temp directory, in the form of a compressed directory in .zip format containing the PDB input files. 

*It is also posible to directly upload the PDB files into the temp folder, but this might take a long time depending on the number of files.*

3.4 Proceed to run the rest of the jupyter notebook as described in the MAGPIE GoogleColab tutorial.

**B. Local-Version**

3.1 Open the MAGPIE Local-Version jupyter notebook 

3.2 Run the Local-Version jupyter notebook. Run the first cell and provide the path to the directory containing the aligned PDB files. Proceed to run the rest of the jupyter notebook as described in the MAGPIE Local-Version tutorial.

