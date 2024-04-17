================================
Using the MAGPIE GUI
================================

I. Run the MAGPIE GUI via the GUI server
========================================

0. Open the MAGPIE GUI server `here <https://magpie-production.up.railway.app/>`_.
------------------------------------------------------------------------------------

Click the button to start uploading your data to the GUI server: 

.. image:: _static/GUI_start.png

1. Upload a zipfile containing the PDBs to be MAGPIED
-------------------------------------------------------

.. image:: _static/GUI_1.png

2. MAGPIE input Prep
--------------------------------------

**Enter values to perform the input prep including binder sequence, binder fasta file, and binder chains. It is also possible to rename your binder chain:**

.. image:: _static/GUI_2-1.png
   

**Select whether your target is a protein or small molecule:**

.. image:: _static/GUI_2-2.png

*If desired, toggle the switch to show advanced options:*

.. image:: _static/GUI_2-3.png

For more information on advanced options, see the supplementary material in the MAGPIE paper: `Rodriguez et al. 2021 <https://doi.org/10.1101/2021.06.29.450229>`_.

A. Enter target small molecule information:
--------------------------------------------

.. image:: _static/GUI_2_A1.png

*If desired, toggle the switch to show advanced options:*

B. Enter target protein information:
-------------------------------------

.. image:: _static/GUI_2_B1.png

*If desired, toggle the switch to show advanced options:*

**Click the RUN MAGPIE INPUT PREP button:**

.. image:: _static/GUI_run2.png

3. Molecule alignment or Protein alignment: 
--------------------------------------------

A. Enter values to perform small alignment and clustering:
----------------------------------------------------------

.. image:: _static/GUI_3_A1.png

B. Enter values to perform protein alignment and clustering:
--------------------------------------------------------------

.. image:: _static/GUI_3_B1.png


4. MAGPIE it!
--------------

.. image:: _static/GUI_4.png

**Click the Plot points in 3D viewer button:**

.. image:: _static/GUI_run4.png

*Example DBSCAN cluster output*

.. image:: _static/GUI_cluster.png

*Example 3D viewer output*

.. image:: _static/GUI_3D.png 

To toggle between 3D viewer settings (Shapely colors, amino colors, H-bonds, charged residues, and DBSCAN hotspots): 

.. image:: _static/GUI_options1.png

To toggle between molecule views: 

.. image:: _static/GUI_options2.png

Download data: 
 
.. image:: _static/GUI_download.png


II. Running the MAGPIE GUI on your local machine
================================================

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

B. Run the MAGPIE GUI via an executable:
---------------------------------------------------
To run the MAGPIE GUI via an exectutable click this `link <https://github.com/glasgowlab/MAGPIE/releases>`_ to download the executable.

C. Build your own MAGPIE executable: 
-------------------------------------
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





