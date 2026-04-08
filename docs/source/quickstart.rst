Quick Start Guide
=================

This guide will walk you through your first collocation workflow using OCSTrack.

Basic Workflow
--------------

A typical OCSTrack workflow consists of five steps:

1. Download observation data (satellite or Argo)
2. Load model outputs
3. Load observation data
4. Perform collocation
5. Analyze results

Example 1: Satellite Altimetry Collocation
-------------------------------------------

Step 1: Download Satellite Data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

   from ocstrack.Observation import get_sat
   
   # Download Jason-3 satellite altimetry data
   get_sat.get_per_sat(
       start_date="2023-01-01",
       end_date="2023-01-07",
       satellite="jason3",
       output_dir="./data/satellite/",
       lat_min=30.0,
       lat_max=45.0,
       lon_min=-80.0,
       lon_max=-60.0
   )

This downloads satellite altimetry data (significant wave height, sea level anomaly) 
for the specified region and time period.

Step 2: Load Model Outputs
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

   from ocstrack.Model.model import SCHISM
   import numpy as np
   
   # Define model configuration
   model_config = {
       'var': 'elevation',
       'startswith': 'out2d_',
       'var_type': '2D'
   }
   
   # Initialize model interface
   model = SCHISM(
       rundir="/path/to/schism/run/",
       model_dict=model_config,
       start_date=np.datetime64("2023-01-01"),
       end_date=np.datetime64("2023-01-07")
   )

Step 3: Load Observation Data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

   from ocstrack.Observation.satellite import SatelliteData
   
   # Load the downloaded satellite data
   sat_data = SatelliteData("./data/satellite/jason3_cropped.nc")
   
   # Optionally filter by time
   sat_data.filter_by_time("2023-01-01", "2023-01-07")

Step 4: Perform Collocation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

   from ocstrack.Collocation.collocate import Collocate
   
   # Create collocation object
   collocator = Collocate(
       model_run=model,
       observation=sat_data,
       n_nearest=4,  # Use 4 nearest model nodes
       temporal_interp=False  # Use nearest neighbor in time
   )
   
   # Run collocation
   result = collocator.run(output_path="./output/collocated_jason3.nc")

Step 5: Analyze Results
^^^^^^^^^^^^^^^^^^^^^^^^

The output is an xarray Dataset containing collocated model and observation data:

.. code-block:: python

   import xarray as xr
   
   # Load collocated results
   ds = xr.open_dataset("./output/collocated_jason3.nc")
   
   # View structure
   print(ds)
   
   # Access variables
   model_ssh = ds['model_var']
   obs_ssh = ds['obs_sla']
   
   # Calculate statistics
   bias = (model_ssh - obs_ssh).mean()
   rmse = ((model_ssh - obs_ssh)**2).mean()**0.5
   
   print(f"Bias: {bias.values:.3f} m")
   print(f"RMSE: {rmse.values:.3f} m")

Example 2: Argo Float 3D Collocation
-------------------------------------

For 3D temperature and salinity profiles:

.. code-block:: python

   from ocstrack.Observation import get_argo
   from ocstrack.Observation.argofloat import ArgoData
   from ocstrack.Model.model import SCHISM
   from ocstrack.Collocation.collocate import Collocate
   import numpy as np
   
   # Download Argo data
   get_argo.get_argo(
       start_date="2023-01-01",
       end_date="2023-01-31",
       region="north_atlantic",
       output_dir="./data/argo/",
       lat_min=35.0,
       lat_max=45.0,
       lon_min=-75.0,
       lon_max=-60.0
   )
   
   # Load Argo data
   argo_data = ArgoData("./data/argo/north_atlantic/processed/")
   
   # Define 3D model configuration
   model_config_3d = {
       'var': 'temperature',
       'startswith': 'temperature_',
       'var_type': '3D_Profile',
       'zcor_var': 'zCoordinates',
       'zcor_startswith': 'zCoordinates_'
   }
   
   # Load model
   model_3d = SCHISM(
       rundir="/path/to/schism/run/",
       model_dict=model_config_3d,
       start_date=np.datetime64("2023-01-01"),
       end_date=np.datetime64("2023-01-31")
   )
   
   # Collocate
   collocator_3d = Collocate(
       model_run=model_3d,
       observation=argo_data,
       n_nearest=3,
       temporal_interp=True  # Use temporal interpolation for profiles
   )
   
   result_3d = collocator_3d.run(output_path="./output/collocated_argo.nc")

Example 3: ADCIRC+SWAN Model
-----------------------------

For ADCIRC+SWAN coupled models:

.. code-block:: python

   from ocstrack.Model.model import ADCSWAN
   
   # Define ADCIRC+SWAN configuration
   model_config_swan = {
       'var': 'swan_HS',
       'startswith': 'swan_HS.63'
   }
   
   # Initialize ADCIRC+SWAN interface
   model_swan = ADCSWAN(
       rundir="/path/to/adcirc/run/",
       model_dict=model_config_swan,
       start_date=np.datetime64("2023-01-01"),
       end_date=np.datetime64("2023-01-07")
   )
   
   # Use same collocation workflow as above
   collocator = Collocate(model_swan, sat_data, n_nearest=4)
   result = collocator.run(output_path="./output/collocated_swan.nc")

Key Parameters Explained
-------------------------

**n_nearest**
   Number of nearest model nodes to use for spatial interpolation (default: 4).
   Higher values provide smoother interpolation but may over-smooth features.

**search_radius**
   Alternative to n_nearest - specify search radius in meters.
   Useful for ensuring spatial consistency.

**temporal_interp**
   * ``False`` (default): Use nearest time step
   * ``True``: Linear interpolation between time steps

**weight_power**
   Exponent for inverse distance weighting (default: 1.0).
   Higher values give more weight to closer nodes.

Next Steps
----------

* Explore the :doc:`examples` for more detailed workflows
* Check the :doc:`api/modules` for complete API documentation
* Learn about :doc:`architecture` for advanced usage
* See :doc:`contributing` to add support for new models

Common Patterns
---------------

**Converting Longitude Conventions**

.. code-block:: python

   from ocstrack.utils import convert_longitude
   
   # Convert from [-180, 180] to [0, 360]
   sat_data.lon = convert_longitude(sat_data.lon, mode=1)
   model.mesh_x = convert_longitude(model.mesh_x, mode=1)

**Filtering Data by Region**

Satellite data can be cropped during download, or you can filter coordinates:

.. code-block:: python

   # Filter after loading
   mask = (sat_data.lat > 30) & (sat_data.lat < 45)
   # Apply mask to your analysis

**Checking Data Availability**

.. code-block:: python

   print(f"Model time range: {model.time[0]} to {model.time[-1]}")
   print(f"Observation time range: {sat_data.time[0]} to {sat_data.time[-1]}")
   print(f"Model has {len(model.files)} output files")
