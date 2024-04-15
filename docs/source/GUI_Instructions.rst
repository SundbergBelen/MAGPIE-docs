================================
Using the MAGPIE GUI
================================

I. Run the MAGPIE GUI via the GUI server
======================================
instructions

II. Running the MAGPIE GUI on your local machine
======================================

MAGPIE is also available for use as a `GUI <https://magpie-production.up.railway.app/>`_. Like the Local-Version of MAGPIE, the MAGPIE GUI can be run on your local machine. The GUI branch releases contain an appropriate executable for Windows, Mac, or linux. If the user would rather create a Conda environment to either build their own executable via pyinstaller or run the GUI via python ./server_local, that is also possible. 

To build your own executable or to run the server locally without an executable, follow the steps below.

Click `here <https://github.com/glasgowlab/MAGPIE/tree/GUI>`_ to navigate to the MAGPIE GUI branch on github. The release tab contains executables for Windows, Mac, or linux: `<https://github.com/glasgowlab/MAGPIE/releases>`_.

A. Run the MAGPIE GUI server locally without an executable: 
--------------------------------------------------------
1. Set up the MAGPIE GUI environment
--------------------------------------

.. code-block:: bash

    git clone git@github.com:glasgowlab/MAGPIE.git
    cd MAGPIE
    git checkout GUI
    conda env create -f environment.yml
    conda activate MAGPE_GUI
   
2. Run the MAGPIE GUI server locally
--------------------------------

.. code-block:: bash

    python server_local.py

Once downloaded, run the GUI executable (.exe file). A terminal should appear and your web browser should open to the GUI. Once both are opened, the GUI is ready to use. All files it creates will be in the current working directory in which the .exe file was opened.

B. Download and run the MAGPIE GUI via an executable:
---------------------------------------------------
1. Set up the MAGPIE GUI environment
-------------------------------------

.. code-block:: bash

   git clone git@github.com:glasgowlab/MAGPIE.git
   cd MAGPIE
   git checkout GUI
   conda env create -f environment.yml
   conda activate MAGPE_GUI

A. Build an executable (Windows):
-----------------------------------

.. code-block:: bash

   pip install pyinstaller
   pyinstaller --clean -F .\server_local.py --add-data "pages/input_prep_page.py;." --add-data "pages/protein_align_page.py;." --add-data "pages/sm_align_page.py;." --add-data "pages/MAGPIE_page.py;." --add-data "logomaker;logomaker" --add-data "pages;pages"

B. Build an executable (Mac/Linux):
------------------------------------
Mac/linux: uninstall pyrosetta before building an EXE. You can make it work if you modify the command below to include the correct files, if you wish.

.. code-block:: bash 

   conda remove pyrosetta

.. code-block:: bash

   pip install pyinstaller
   pyinstaller --clean -F server_local.py --add-data="pages/input_prep_page.py:." --add-data="pages/protein_align_page.py:." --add-data="pages/sm_align_page.py:." --add-data="pages/MAGPIE_page.py:." --add-data="logomaker:logomaker" --add-data="pages:pages" --hidden-import='PIL._tkinter_finder' --add-data="logomaker/src:logomaker/src"





