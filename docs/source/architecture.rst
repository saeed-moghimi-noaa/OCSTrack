Architecture Overview
=====================

OCSTrack Design
---------------

OCSTrack follows an object-oriented design with clear separation of concerns across three main modules:

Module Structure
----------------

.. code-block:: text

   ocstrack/
   ├── Observation/      # Data acquisition and handling
   │   ├── satellite.py  # SatelliteData class
   │   ├── argofloat.py  # ArgoData class
   │   ├── get_sat.py    # Download functions
   │   ├── get_argo.py   # Download functions
   │   └── urls.py       # Data source endpoints
   ├── Model/            # Model output interfaces
   │   └── model.py      # SCHISM, ADCSWAN classes
   ├── Collocation/      # Core algorithms
   │   ├── collocate.py  # Main Collocate class
   │   ├── spatial.py    # Spatial interpolation
   │   ├── temporal.py   # Temporal matching
   │   └── output.py     # NetCDF formatting
   └── utils.py          # Utilities

Data Flow
---------

.. code-block:: text

   ┌─────────────────┐     ┌──────────────────┐
   │  Observations   │     │  Model Outputs   │
   │  (Satellite/    │     │  (SCHISM/        │
   │   Argo)         │     │   ADCIRC)        │
   └────────┬────────┘     └────────┬─────────┘
            │                       │
            │    ┌──────────────────┤
            │    │                  │
            ▼    ▼                  ▼
   ┌─────────────────┐    ┌─────────────────┐
   │ Observation     │    │ Model Interface │
   │ Data Classes    │    │ Classes         │
   └────────┬────────┘    └────────┬─────────┘
            │                      │
            └──────────┬───────────┘
                       │
                       ▼
            ┌──────────────────────┐
            │  Collocate Engine    │
            │  - Spatial locator   │
            │  - Temporal matching │
            │  - Interpolation     │
            └──────────┬───────────┘
                       │
                       ▼
            ┌──────────────────────┐
            │  Collocated NetCDF   │
            │  - Model values      │
            │  - Observation values│
            │  - Metadata          │
            └──────────────────────┘

Key Design Patterns
-------------------

**Adapter Pattern**
   Model classes (SCHISM, ADCSWAN) adapt different model output formats to a common interface.

**Strategy Pattern**
   Temporal matching supports multiple strategies (nearest, interpolated) selected at runtime.

**Factory Pattern**
   Data downloaders create appropriate data objects based on source type.

Extensibility Points
--------------------

Adding New Models
^^^^^^^^^^^^^^^^^

Implement the model interface in ``ocstrack/Model/model.py``:

* ``__init__``: Configuration and file selection
* ``load_variable``: Load model variable from file
* Properties: ``mesh_x``, ``mesh_y``, ``mesh_depth``, ``files``, ``time``

Adding New Observations
^^^^^^^^^^^^^^^^^^^^^^^

Create a new class in ``ocstrack/Observation/``:

* Properties: ``time``, ``lon``, ``lat``, plus data variables
* Method: ``filter_by_time``
* Compatible with ``Collocate`` class

Adding Spatial Methods
^^^^^^^^^^^^^^^^^^^^^^

Extend ``ocstrack/Collocation/spatial.py`` with new interpolation algorithms.

Dependencies
------------

**Core Scientific Stack**

* xarray: Labeled array handling, NetCDF I/O
* numpy: Array operations
* scipy: KDTree for spatial searching

**Performance**

* dask: Lazy loading, parallel computation
* tqdm: Progress tracking for long operations

**Data Access**

* requests: HTTP downloads
* netcdf4/h5netcdf: NetCDF backends

Performance Considerations
--------------------------

* Uses xarray's lazy loading to handle large model outputs
* Spatial queries optimized with scipy KDTree (O(log n) lookups)
* Temporal queries use binary search on sorted time arrays
* Memory-efficient file-by-file processing for 3D collocation

Future Enhancements
-------------------

Planned architectural improvements:

* Parallel collocation using Dask distributed
* Streaming collocation for near-real-time applications
* Plugin system for custom models and observations
* GPU acceleration for spatial interpolation

For implementation details, see the API reference.
