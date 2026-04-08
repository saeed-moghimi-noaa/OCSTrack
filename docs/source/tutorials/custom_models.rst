Adding Custom Model Support
============================

This guide shows how to extend OCSTrack to support new ocean or wave models.

Overview
--------

OCSTrack currently supports SCHISM and ADCIRC+SWAN, but the architecture is designed 
for extensibility. This guide walks through adding support for a new model type.

Model Interface Requirements
-----------------------------

Your custom model class should implement:

* ``__init__(rundir, model_dict, start_date, end_date)``
* ``load_variable(path)`` - Load model variable from file
* Properties: ``mesh_x``, ``mesh_y``, ``mesh_depth``, ``files``, ``time``

Example Structure
-----------------

.. code-block:: python

   class CustomModel:
       def __init__(self, rundir, model_dict, start_date, end_date):
           self.rundir = rundir
           self.model_dict = model_dict
           self.start_date = start_date
           self.end_date = end_date
           
           # Validate configuration
           self._validate_model_dict()
           
           # Select relevant output files
           self._files = self._select_model_files()
           
           # Load mesh information
           self._mesh_x, self._mesh_y, self._mesh_depth = self._load_mesh()
       
       def _validate_model_dict(self):
           # Check required keys exist
           required_keys = ['var', 'startswith']
           for key in required_keys:
               if key not in self.model_dict:
                   raise ValueError(f"Missing required key: {key}")
       
       def _select_model_files(self):
           # Logic to find and filter output files
           pass
       
       def _load_mesh(self):
           # Load mesh coordinates and depth
           pass
       
       def load_variable(self, path):
           # Load and return xarray DataArray
           pass
       
       @property
       def mesh_x(self):
           return self._mesh_x
       
       # ... other properties

Full tutorial coming soon!
