Contributing to OCSTrack
=========================

We welcome contributions to OCSTrack! This guide will help you get started.

Ways to Contribute
------------------

* **Report bugs**: Open an issue on GitHub
* **Request features**: Suggest new functionality
* **Improve documentation**: Fix typos, add examples, clarify instructions
* **Submit code**: Bug fixes, new features, performance improvements
* **Add model support**: Extend to new ocean/wave models

Getting Started
---------------

1. Fork the repository on GitHub
2. Clone your fork locally:

.. code-block:: bash

   git clone https://github.com/YOUR_USERNAME/OCSTrack.git
   cd OCSTrack

3. Create a development environment:

.. code-block:: bash

   conda create -n ocstrack-dev python=3.10
   conda activate ocstrack-dev
   pip install -e .[dev]

4. Create a branch for your changes:

.. code-block:: bash

   git checkout -b feature/my-new-feature

Development Guidelines
----------------------

Code Style
^^^^^^^^^^

* Follow PEP 8 style guide
* Use descriptive variable names
* Maximum line length: 100 characters
* Use type hints for function signatures

Docstring Format
^^^^^^^^^^^^^^^^

Use NumPy-style docstrings:

.. code-block:: python

   def my_function(param1, param2):
       """
       Brief description of function.
       
       Longer description if needed. Explain the purpose and behavior.
       
       Parameters
       ----------
       param1 : type
           Description of param1
       param2 : type
           Description of param2
       
       Returns
       -------
       return_type
           Description of return value
       
       Examples
       --------
       >>> result = my_function(val1, val2)
       >>> print(result)
       Expected output
       """
       pass

Testing
^^^^^^^

* Add tests for new features
* Ensure existing tests pass:

.. code-block:: bash

   pytest tests/

* Run pylint to check code quality:

.. code-block:: bash

   pylint ocstrack/

Submitting Changes
------------------

1. Commit your changes with clear messages:

.. code-block:: bash

   git add .
   git commit -m "Add feature: brief description"

2. Push to your fork:

.. code-block:: bash

   git push origin feature/my-new-feature

3. Open a Pull Request on GitHub

4. Describe your changes and link any related issues

Pull Request Checklist
----------------------

Before submitting:

* [ ] Code follows style guidelines
* [ ] Docstrings added/updated
* [ ] Tests added/updated
* [ ] All tests pass
* [ ] Documentation updated if needed
* [ ] Changelog entry added (if applicable)

Code of Conduct
---------------

* Be respectful and inclusive
* Welcome newcomers
* Focus on constructive feedback
* Assume good intentions

Questions?
----------

* Open a discussion on GitHub
* Contact: felicio.cassalho@noaa.gov

Thank you for contributing to OCSTrack!
