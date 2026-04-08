Acknowledgments
===============

OCSTrack Development Team
--------------------------

**Lead Developer**
   Felicio Cassalho, NOAA Office of Coast Survey

**Contributors**
   NOAA OCS Modeling Team

Funding & Support
-----------------

This work is supported by:

* NOAA Office of Coast Survey
* NOAA National Ocean Service

Inspiration & Related Tools
---------------------------

OCSTrack was inspired by and builds upon concepts from:

* **WW3-tools**: MATLAB-based collocation tools for WaveWatch3 
  (https://github.com/NOAA-EMC/WW3-tools)
* **wave-tools**: ERDC wave model validation tools
  (https://github.com/erdc/wave-tools)

Data Sources
------------

OCSTrack integrates data from:

* **NOAA CoastalWatch**: Satellite altimetry data
  (https://coastwatch.noaa.gov/)
* **Euro Argo**: Argo float profiles
  (https://fleetmonitoring.euro-argo.eu/)

Software Dependencies
---------------------

OCSTrack relies on excellent open-source scientific Python packages:

* **xarray**: Labeled multi-dimensional arrays
* **NumPy**: Fundamental array computing
* **SciPy**: Scientific computing tools
* **Dask**: Parallel computing
* **netCDF4**: NetCDF file I/O

Model Communities
-----------------

Thanks to the ocean modeling communities for:

* **SCHISM**: https://github.com/schism-dev/schism
* **ADCIRC**: https://adcirc.org/

Contact
-------

Questions, suggestions, or collaborations:

* Email: felicio.cassalho@noaa.gov
* GitHub Issues: https://github.com/noaa-ocs-modeling/OCSTrack/issues
* GitHub Discussions: https://github.com/noaa-ocs-modeling/OCSTrack/discussions

Citation
--------

If you use OCSTrack in your research, please cite:

.. code-block:: bibtex

   @software{ocstrack2024,
     author = {Cassalho, Felicio and {NOAA OCS Modeling Team}},
     title = {OCSTrack: Ocean Circulation and Satellite Tracking Collocation Tool},
     year = {2024},
     publisher = {GitHub},
     url = {https://github.com/noaa-ocs-modeling/OCSTrack}
   }
