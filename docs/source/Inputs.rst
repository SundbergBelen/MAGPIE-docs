Required inputs
---------------

**PDB files:** these should be aligned on the target ligands. Two examples are provided on GitHub, one for protein-protein interactions and one for small molecule-protein interactions. If you choose to upload your own PDB files, you will first need to clean, standardize, and align input PDB files for seamless usage in MAGPIE (See the `Preparing your own dataset for use in MAGPIE <https://magpie-docs.readthedocs.io/en/latest/Preparing_samples.html>`_ and `Helper Scripts <https://magpie-docs.readthedocs.io/en/latest/HelperScripts.html>`_ sections of this documentation).

**Target chain ID from PDB:** the program uses the first file in the directory to upload the target ligand structure.

**Protein binder chain ID from PDB:** this chain identifier must be the same across all PDB files.

**Target type:** indicate whether the target ligand is a small molecule or a protein.

**Target residue index (for protein ligands) or unique atom names (for small molecule ligands):** provide the target residue indices for proteins or unique atom names for small molecules. Alternatively, you can input 'all' to consider all AAs/heavy atoms.