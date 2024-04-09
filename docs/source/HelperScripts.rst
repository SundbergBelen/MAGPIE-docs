===============
Helper Scripts
===============

To use your own PDB files with MAGPIE GoogleColab or Local-Version, you will need to clean, standardize, and align the input PDB files, by using helper scripts ``MAGPIE_input_prep.py``, ``align_protein_chain.py``, and ``align_small_molecule.py`` which can be downloaded from the `GitHub repository <https://github.com/glasgowlab/MAGPIE>`_ if you are using the GoogleColab version of MAGPIE. If you have downloaded the Local-Version of MAGPIE, these scripts are included in the downloaded repository. Use of the MAGPIE helper scripts requires python to be installed on your local machine. For information on how to install Python, please visit `https://www.python.org/downloads/ <https://www.python.org/downloads/>`_.

I. ``MAGPIE_input_prep.py`` 
========================
This script allows the user to input files or directories with options to define target ligands and protein binders by chain, protein sequence (with percent sequence identity), ligand name (for small molecule targets), and search radius around the target. The alignment scripts align the protein-ligand complexes on the target ligand for use with MAGPIE, returning subsets of complexes for small molecule ligands as determined by user-defined all-atom RMSD. 

To list the arguments of the ``MAGPIE_input_prep.py`` script, run the following command in the terminal:

.. code-block:: bash

    python MAGPIE_input_prep.py help


Usage
------
MAGPIE_input_prep.py [-h] [-S BINDER_SEQS] [-s TARGET_PROTEIN_SEQS] [-F BINDER_SEQ_FA] [-f TARGET_PROTEIN_SEQ_FA] [-L TARGET_SM_3_NAMES]
[-I TARGET_SM_INDEX] [-C BINDER_CHAINS] [-c TARGET_PROTEIN_CHAINS] [-l TARGET_SM_CHAINS] [-U {chains,sequences}] [-u {chains,name}]
[-d SEQ_IDENTITY] -i INPUT_PATH -o OUTPUT_PATH [-N TARGET_PROTEIN_CHAIN_RENAME] [-n TARGET_SM_CHAIN_RENAME] [-b BINDER_CHAIN_RENAME]
[-t] [-T] [-r SM_LIGAND_REFERENCE_PATH] [-B BOND_LENGTH] [-m SEARCH_RADIUS] [-M MESH_SEARCH] [-A {1v1,MSA}] [-a SEQ_TARGET_REF_PDB]

Argument definitions
---------------------
1. -h, --help            show this help message and exit

2. -S BINDER_SEQS, --binder_seqs BINDER_SEQS
                        The sequence(s) of the binder used for identification.

3. -s TARGET_PROTEIN_SEQS, --target_protein_seqs TARGET_PROTEIN_SEQS
                        The sequence(s) of the target protein used for identification.

4. -F BINDER_SEQ_FA, --binder_seq_fa BINDER_SEQ_FA
                        The sequence file (fasta format) of the binder used for identification.

5. -f TARGET_PROTEIN_SEQ_FA, --target_protein_seq_fa TARGET_PROTEIN_SEQ_FA
                        The sequence file (fasta format) of the target protein used for identification.

6. -L TARGET_SM_3_NAMES, --target_sm_3_names TARGET_SM_3_NAMES
                        The three letter code of the small molecule(s).

7. -I TARGET_SM_INDEX, --target_sm_index TARGET_SM_INDEX
                        The index of the small molecule(s). Must be used in tandem with chain or name.

8. -C BINDER_CHAINS, --binder_chains BINDER_CHAINS
                        The chain(s) of the binder used for identification.

9. -c TARGET_PROTEIN_CHAINS, --target_protein_chains TARGET_PROTEIN_CHAINS
                        The chains of the target protein used for identification.

10. -l TARGET_SM_CHAINS, --target_sm_chains TARGET_SM_CHAINS
                        The chain(s) of the small molecule used for identification.

11. -U {chains,sequences}, --search_first_protein {chains,sequences}
                        If using both chains and sequences search, what should be used to be filtered first? Choices: "chains" or "sequences" Default: "chains"

12. -u {chains,name}, --search_first_sm {chains,name}
                        If using both chains and sequences search, what should be used to be filtered first? Choices: "chains" or "sequences" Default: "chains"

13. -n TARGET_SM_CHAIN_RENAME, --target_sm_chain_rename TARGET_SM_CHAIN_RENAME
                        What the target small molecule output chain should be named. Default: "B"

14. -N TARGET_PROTEIN_CHAIN_RENAME, --target_protein_chain_rename TARGET_SM_CHAIN_RENAME
                        What the target protein output chain should be named. Default: "A"

15. -b BINDER_CHAIN_RENAME, --binder_chain_rename BINDER_CHAIN_RENAME
                        What the binder output chain should be named. Default: "C" 

16. -t TAKE_FIRST_SM_ONLY, --take_first_sm_only TAKE_FIRST_SM_ONLY
                        Should we only take the first instance of the ligand?

17. -T NAME_SM_ATOMS_SAME, --name_sm_atoms_same NAME_SM_ATOMS_SAME
                        Should we rename all matching ligands with the same atom names? Uses the first file as a reference.

18. -r SM_LIGAND_REFERENCE_PATH, --sm_ligand_reference_path SM_LIGAND_REFERENCE_PATH
                        Path of the reference file for renaming the small molecule ligands. Default is the first file found with Python’s list directory function.

19. -B BOND_LENGTH, --bond_length BOND_LENGTH
                        Distance that defines a bond between 2 atoms for chemical graphs. Default: 2.1

20. -m SEARCH_RADIUS, --search_radius SEARCH_RADIUS
                        Distance that is considered for finding neighboring atoms in the mesh search. Default: 8

21. -M MESH_SEARCH, --mesh_search MESH_SEARCH
                        The chains, sequence(s), small molecule name(s), small molecule index(es) for the mesh filter. Example: 'A,B;AWTRWARE,AWAWAWAW;TPA,ATP;1,2'

22. -A SEQ_TARGET_ALIGN, --seq_target_align SEQ_TARGET_ALIGN
                        Should we align the target protein in sequence space? Results in PDB numbering via alignment. Do not use it for small molecule ligands. Choices: "1v1", "MSA"

23. -a SEQ_TARGET_REF_PDB, --seq_target_ref_pdb SEQ_TARGET_REF_PDB
                        Reference structure for target protein in seq_target_align.

24. -d SEQ_IDENTITY, --seq_identity SEQ_TARGET_REF_PDB
                        Sequence identity threshold for finding similar chains. Default: 95%

Example
--------
.. code-block:: bash

    python ~/MAGPIE/MAGPIE_input_prep.py -i <input_directory> -o <output_directory> -L COA -M 'A,B;;COA;'

**For more examples see the MAGPIE supplementary material in** `Rodriguez et al. 2023 <https://www.biorxiv.org/content/10.1101/2023.09.04.556273v2>`_

II. ``align_protein_chain.py`` 
===========================
This script is used to align protein chains from different PDB files based on a specified chain identifier. The alignment is done using PyMOL's cealign command, which performs a sequence-independent alignment of two objects based on their shapes. The function takes four arguments. The script works by iterating over all PDB files in the specified directory, loading each file into PyMOL, and aligning the specified chain in the current file to the same chain in the first file. The RMSD value of each alignment is calculated and written to a CSV file along with the name of the PDB file. If the RMSD value is less than or equal to the threshold, the aligned structure is saved as a new PDB file in the output directory.

Usage
------
align_protein_chain.py [-h] -c CHAIN_TO_ALIGN [-T RMSD_THRESHOLD] -i INPUT_PATH -o OUTPUT_PATH

Argument definitions
---------------------
1. -h, --help            show this help message and exit

2. -c CHAIN_TO_ALIGN, --chain_to_align CHAIN_TO_ALIGN
                        chain identifier for chains to align

3. -T RMSD_THRESHOLD, --rmsd_threshold RMSD_THRESHOLD
                        RMSD Threshold for filtering.

4. -i INPUT_PATH, --input_path INPUT_PATH
                        path of the input directory
5. -o OUTPUT_PATH, --output_path OUTPUT_PATH
                        path of the output directory

Example
--------

.. code-block:: bash

    python ~/MAGPIE/align_protein_chain.py -c B -T 2.5 -i <input_directory> -o <output_directory>


III. ``align_small_molecule.py``
============================
This script is used to align small molecules in different PDB  files based on a specified chain identifier. The alignment is done using PyMOL's align command, which performs a sequence-dependent alignment of two objects based on their atom types and bond connectivity.  The function works by iterating over all PDB files in the specified directory, loading each file into PyMOL, and aligning the specified chain in the current file to the same chain in the first file. The RMSD value of each alignment is calculated. If the RMSD value is less than or equal to the threshold, the aligned structure is saved as a new PDB file in the output directory. If the RMSD value is greater than the threshold, a new reference structure is created and the process continues with the next PDB file.  The function also creates a directory for each reference structure and saves the aligned structures in the corresponding directory. If the pair_fit argument is set to True, the function will use the pair_fit command for alignment, which aligns two objects based on a set of atom pairs. This can be useful when the atom names or numbers differ too much between the two structures. 

The pair_fit function is only recommended to be used if MAGPIE_input_prep.py is used first. 

Usage
------
align_small_molecule.py [-h] -c CHAIN_TO_ALIGN [-T RMSD_THRESHOLD] -i INPUT_PATH -o OUTPUT_PATH [-p {True,False}]

Argument definitions
---------------------
1. -h, --help            show this help message and exit

2. -c CHAIN_TO_ALIGN, --chain_to_align CHAIN_TO_ALIGN
                       chain identifier for chains to align

3. -T RMSD_THRESHOLD, --rmsd_threshold RMSD_THRESHOLD
                        RMSD Threshold Difference

4. -i INPUT_PATH, --input_path INPUT_PATH
                        path of the input directory

5. -o OUTPUT_PATH, --output_path OUTPUT_PATH
                        path of the output directory

6.  -p {True,False}, --pair_fit {True,False}
                        use pair_fit instead

Example
--------
.. code-block:: bash

    python ~/MAGPIE/align_small_molecule.py -c B -T 2.5 -i <input_directory> -o <output_directory> -p True