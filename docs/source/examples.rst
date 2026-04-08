Examples
========

This page links to the example scripts and notebooks included with OCSTrack.

Example Scripts
---------------

The ``examples/`` directory contains complete working scripts:

SCHISM with Argo Floats
^^^^^^^^^^^^^^^^^^^^^^^^

**File**: ``examples/SCHISM_ArgoFloat.py``

Demonstrates 3D collocation of Argo float temperature profiles with SCHISM model outputs.

**Key features**:

* Downloads Argo data from GDAC
* Loads 3D SCHISM temperature fields
* Handles vertical coordinate interpolation
* Exports collocated NetCDF file

SCHISM+WWM with Satellite Altimetry
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**File**: ``examples/SCHISMWWM_SatAlt.py``

Collocates satellite altimetry (significant wave height) with SCHISM-WWMIII coupled model outputs.

**Key features**:

* Downloads Jason-3/Sentinel-3 altimetry data
* Loads SCHISM wave model outputs
* Spatial and temporal collocation
* Statistical validation

ADCIRC+SWAN with Satellite Altimetry
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**File**: ``examples/ADCIRCSWAN_SatAlt.py``

Uses the ADCSWAN model interface to collocate satellite observations with ADCIRC+SWAN outputs.

**Key features**:

* ADCIRC+SWAN specific file handling
* Single-file model output format
* Wave height validation

Jupyter Notebooks
-----------------

Plot Collocated Results
^^^^^^^^^^^^^^^^^^^^^^^^

**File**: ``examples/Plot_Collocated.ipynb``

Interactive notebook demonstrating visualization of collocated data.

**Includes**:

* Loading collocated NetCDF files
* Time series plots
* Scatter plots (model vs. observations)
* Statistical metrics (bias, RMSE, correlation)
* Spatial distribution maps

Running the Examples
--------------------

1. Clone the repository:

.. code-block:: bash

   git clone https://github.com/noaa-ocs-modeling/OCSTrack.git
   cd OCSTrack/examples

2. Edit file paths in the scripts to point to your data locations

3. Run a script:

.. code-block:: bash

   python SCHISM_ArgoFloat.py

4. Or open the notebook:

.. code-block:: bash

   jupyter notebook Plot_Collocated.ipynb

Example Data Requirements
--------------------------

The examples require:

* **Model outputs**: SCHISM or ADCIRC+SWAN run directories
* **Internet connection**: For downloading observation data
* **Storage**: ~100 MB for satellite data, ~500 MB for Argo data (depending on region/time)

Customizing Examples
--------------------

To adapt examples for your use case:

1. **Update time ranges**: Modify ``start_date`` and ``end_date``
2. **Change geographic region**: Adjust ``lat_min``, ``lat_max``, ``lon_min``, ``lon_max``
3. **Select different satellite**: Change ``satellite="jason3"`` to other missions
4. **Modify model paths**: Point to your model run directory
5. **Adjust collocation parameters**: Change ``n_nearest``, ``temporal_interp``, etc.

Need Help?
----------

If you encounter issues with the examples:

1. Check that all file paths are correct
2. Verify your model outputs are in the expected format
3. Ensure you have sufficient disk space for downloads
4. See :doc:`installation` for dependency troubleshooting
5. Open an issue on GitHub: https://github.com/noaa-ocs-modeling/OCSTrack/issues
