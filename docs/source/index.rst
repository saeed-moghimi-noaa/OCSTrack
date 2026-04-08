OCSTrack Documentation
======================

**Ocean Circulation and Satellite Tracking Collocation Tool**

OCSTrack is an object-oriented Python package for the along-track collocation of satellite (2D) 
and ArgoFloat (3D) data with ocean circulation and wave model outputs. It simplifies the process 
of aligning diverse datasets, making it easier to compare and analyze satellite observations 
against model simulations.

.. image:: https://img.shields.io/badge/python-3.10%2B-blue.svg
   :target: https://www.python.org/
   :alt: Python Version

.. image:: https://img.shields.io/badge/License-MIT-yellow.svg
   :target: https://github.com/noaa-ocs-modeling/OCSTrack/blob/main/LICENSE.txt
   :alt: License

Key Features
------------

* **Multi-source Satellite Altimetry**: Integrates with NOAA CoastalWatch data (Jason-2/3, Sentinel-3A/B, Sentinel-6A, CryoSat-2, SARAL, SWOT)
* **3D Profile Data**: Supports Euro Argo dataset for temperature and salinity collocation
* **Multiple Model Support**: Works with SCHISM, ADCIRC+SWAN, and extensible to other models
* **Advanced Collocation**: Geocentric spatial locator with inverse distance weighting
* **Flexible Temporal Matching**: Nearest neighbor or linear interpolation
* **Automated Data Retrieval**: Built-in downloaders for satellite and Argo data

Quick Start
-----------

Install OCSTrack:

.. code-block:: bash

   conda create -n ocstrack -c conda-forge python=3.10 numpy xarray scipy tqdm requests netcdf4 h5netcdf dask
   conda activate ocstrack
   pip install ocstrack

Basic usage example:

.. code-block:: python

   from ocstrack.Model.model import SCHISM
   from ocstrack.Observation.satellite import SatelliteData
   from ocstrack.Collocation.collocate import Collocate
   import numpy as np

   # Load model outputs
   model = SCHISM(
       rundir="/path/to/model/",
       model_dict={'var': 'elevation', 'startswith': 'out2d_', 'var_type': '2D'},
       start_date=np.datetime64("2023-01-01"),
       end_date=np.datetime64("2023-01-07")
   )

   # Load satellite observations
   sat_data = SatelliteData("./satellite_data.nc")

   # Collocate model and observations
   collocator = Collocate(model, sat_data, n_nearest=4)
   result = collocator.run(output_path="collocated.nc")

.. toctree::
   :maxdepth: 2
   :caption: User Guide
   
   installation
   quickstart
   tutorials/index
   examples

.. toctree::
   :maxdepth: 2
   :caption: API Reference
   
   api/modules

.. toctree::
   :maxdepth: 1
   :caption: Developer Guide
   
   contributing
   architecture
   changelog

.. toctree::
   :maxdepth: 1
   :caption: About
   
   license
   acknowledgments

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
