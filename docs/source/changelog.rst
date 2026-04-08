Changelog
=========

All notable changes to OCSTrack will be documented in this file.

The format is based on `Keep a Changelog <https://keepachangelog.com/en/1.0.0/>`_,
and this project adheres to `Semantic Versioning <https://semver.org/spec/v2.0.0.html>`_.

[Unreleased]
------------

Added
^^^^^
* Comprehensive Sphinx documentation
* Installation guide with multiple methods
* Quick start tutorial
* API reference auto-generated from docstrings
* Contributing guidelines
* Architecture overview

[0.1.0] - 2024
--------------

Initial release

Added
^^^^^
* Satellite altimetry data support (Jason-2/3, Sentinel-3A/B, Sentinel-6A, CryoSat-2, SARAL, SWOT)
* Argo float 3D profile support
* SCHISM model interface with 2D and 3D support
* ADCIRC+SWAN model interface
* Geocentric spatial locator with inverse distance weighting
* Temporal matching (nearest neighbor and linear interpolation)
* Automated data download from NOAA CoastalWatch and Euro Argo
* NetCDF output format for collocated data
* Example scripts for common workflows
* Basic README documentation
* pytest test suite
* GitHub Actions CI/CD

Known Issues
^^^^^^^^^^^^
* WaveWatch3 support not yet implemented
* Limited documentation beyond code examples

[0.0.1] - 2023
--------------

Initial development version (not publicly released)
