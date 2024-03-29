Using MAGPIE with Local-Version
=================================

The following are a set of command-line-centric instructions for installing
pySCA on Linux, Windows, and macOS operating systems.

1. Install Dependencies
=======================

Choose the set of instructions in this section based on your operating system.

Linux (Ubuntu 18.04)
--------------------

Before installing pySCA, install the following packages from your package
repository:

1) Python 3
2) Pip
3) GCC

.. code-block:: bash

   sudo apt-get install python3 python3-pip git gcc

2. Download Code
================

The MAGPIE Local-Version package, tutorials, and associated scripts are available for download
from the `GitHub repository <https://github.com/glasgowlab/MAGPIE>`_. There
are several options for doing so.

A. Use Git
----------

If you have :code:`git` installed on your system, you can use it to clone the
repository from GitHub. 

cd into the directory where you would like to download the code.
From the command line, run:

..code-block:: bash

   cd /path/to/directory

.. code-block:: bash

   git clone https://github.com/glasgowlab/MAGPIE.git

The code will now be downloaded in a directory called `MAGPIE`.

B. (OR) Download from the Website
---------------------------------

Though not recommended, you can also download the source code from the GitHub
website. Click the green "Clone or download" tab pictured below to obtain the
latest code.

.. image:: _static/github-download-screenshot.png

3. Getting Started with MAGPIE Local-Version 
================

The Local-Version of MAGPIE is a standalone version of the MAGPIE code that can be run on a local machine.  

It is always recommended that you create a conda environment for any project you are working on. This will help you to keep your dependencies separate from other projects. To create a new conda environment, run the following command:

.. code-block:: bash

   conda create -n magpie python=3.7

To activate the environment, run:

.. code-block:: bash

   conda activate magpie

Running MAGPIE Local-Version requires installation of Jupyter notebooks. For more on how Jupyter notebooks work, see: `<https://jupyter.org>`_.

To install Jupyter notebooks, run the following command within your conda environment:

.. code-block:: bash

   pip install jupyter

To begin running the MAGPIE Local-Version, navigate to the directory where you downloaded the code and open the jupyter notebook via the following command:

.. code-block:: bash

   cd /path/to/MAGPIE

.. code-block:: bash
    
   jupyter notebook
