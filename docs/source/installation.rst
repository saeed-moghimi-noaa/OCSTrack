Installation
============

Prerequisites
-------------

OCSTrack requires:

* Python 3.10 or higher
* conda or mamba package manager (recommended)

Quick Install
-------------

The easiest way to install OCSTrack is via pip:

.. code-block:: bash

   # Create a new environment (recommended)
   conda create -n ocstrack -c conda-forge python=3.10 numpy xarray scipy tqdm requests netcdf4 h5netcdf dask
   conda activate ocstrack
   
   # Install OCSTrack
   pip install ocstrack

Install from Source
-------------------

For development or to get the latest features:

.. code-block:: bash

   # Clone the repository
   git clone https://github.com/noaa-ocs-modeling/OCSTrack.git
   cd OCSTrack
   
   # Create environment
   conda create -n ocstrack -c conda-forge python=3.10 numpy xarray scipy tqdm requests netcdf4 h5netcdf dask
   conda activate ocstrack
   
   # Install in development mode
   pip install -e .

Install with Development Tools
-------------------------------

If you plan to contribute to OCSTrack:

.. code-block:: bash

   # Install with development dependencies
   pip install -e .[dev]
   
   # This includes pytest, pylint, and other development tools

Dependencies
------------

Core dependencies (automatically installed):

* **numpy**: Array operations
* **xarray**: NetCDF and labeled array handling
* **scipy**: Scientific computing utilities
* **tqdm**: Progress bars
* **requests**: HTTP library for data downloads
* **netcdf4**: NetCDF file I/O
* **h5netcdf**: Alternative NetCDF backend
* **dask**: Parallel computing

Optional dependencies:

* **gsw**: Gibbs SeaWater toolbox for accurate depth calculations (recommended for Argo)

.. code-block:: bash

   conda install -c conda-forge gsw

Verify Installation
-------------------

Test your installation:

.. code-block:: python

   import ocstrack
   from ocstrack.Observation.satellite import SatelliteData
   from ocstrack.Model.model import SCHISM
   from ocstrack.Collocation.collocate import Collocate
   
   print("OCSTrack imported successfully!")

Troubleshooting
---------------

**Issue**: ``ImportError: No module named 'netcdf4'``

**Solution**: Install netcdf4 via conda:

.. code-block:: bash

   conda install -c conda-forge netcdf4

**Issue**: ``ModuleNotFoundError: No module named 'xarray'``

**Solution**: Ensure all dependencies are installed:

.. code-block:: bash

   pip install -r requirements.txt

**Issue**: Conflicts with existing packages

**Solution**: Use a fresh conda environment:

.. code-block:: bash

   conda create -n ocstrack_clean python=3.10
   conda activate ocstrack_clean
   # Then install OCSTrack
