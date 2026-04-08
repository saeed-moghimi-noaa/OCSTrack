# Testing OCSTrack Documentation Locally

## Quick Start

The documentation has been successfully built! Follow these steps to view it:

### 1. View the Documentation

Open the built HTML documentation in your web browser:

```bash
# From the OCSTrack root directory
firefox docs/build/html/index.html
# or
google-chrome docs/build/html/index.html
# or
open docs/build/html/index.html  # macOS
```

Alternatively, start a local web server:

```bash
cd docs/build/html
python -m http.server 8000
```

Then open http://localhost:8000 in your browser.

### 2. Make Changes and Rebuild

If you want to modify the documentation:

```bash
# Edit files in docs/source/
# For example: docs/source/installation.rst

# Rebuild the documentation
cd docs
make html

# View changes by refreshing your browser
```

### 3. Clean Build (if needed)

If you encounter issues or want a fresh build:

```bash
cd docs
make clean
make html
```

## What Was Installed

The following Sphinx setup has been created:

### Directory Structure

```
OCSTrack/
├── docs/
│   ├── source/               # Documentation source files
│   │   ├── index.rst         # Main page
│   │   ├── installation.rst  # Installation guide
│   │   ├── quickstart.rst    # Quick start tutorial
│   │   ├── examples.rst      # Examples page
│   │   ├── contributing.rst  # Contributing guide
│   │   ├── architecture.rst  # Architecture overview
│   │   ├── changelog.rst     # Changelog
│   │   ├── license.rst       # License info
│   │   ├── acknowledgments.rst # Credits
│   │   ├── conf.py           # Sphinx configuration
│   │   ├── api/              # Auto-generated API docs
│   │   │   ├── modules.rst
│   │   │   ├── ocstrack.rst
│   │   │   ├── ocstrack.Collocation.rst
│   │   │   ├── ocstrack.Model.rst
│   │   │   └── ocstrack.Observation.rst
│   │   └── tutorials/        # Tutorial pages
│   │       ├── index.rst
│   │       ├── satellite_collocation.rst
│   │       ├── argo_collocation.rst
│   │       └── custom_models.rst
│   ├── build/html/           # Built HTML documentation
│   ├── Makefile              # Build commands
│   └── requirements.txt      # Documentation dependencies
```

### Installed Extensions

- **sphinx**: Core documentation system
- **sphinx-rtd-theme**: Read the Docs theme (clean, professional)
- **sphinx-autodoc-typehints**: Type hint support
- **sphinxcontrib-napoleon**: NumPy/Google docstring support
- **nbsphinx**: Jupyter notebook support
- **myst-parser**: Markdown support

### Configuration Highlights

The `docs/source/conf.py` includes:

- ✅ NumPy-style docstring support
- ✅ Auto-generated API documentation
- ✅ Links to NumPy, SciPy, xarray docs (intersphinx)
- ✅ Math equation support (MathJax)
- ✅ Read the Docs theme
- ✅ Accessibility features (508 compliance)
- ✅ Mock imports (docs build without installing all dependencies)

## Documentation Features

### 1. API Reference

The API documentation is automatically generated from your docstrings:

- **Observation Module**: SatelliteData, ArgoData, data downloaders
- **Model Module**: SCHISM, ADCSWAN interfaces
- **Collocation Module**: Collocate, spatial/temporal methods
- **Utilities**: Helper functions

### 2. User Guide

- Installation instructions (pip, conda, source)
- Quick start with complete examples
- Tutorials (placeholders for now, ready to expand)
- Examples from your `examples/` directory

### 3. Developer Guide

- Contributing guidelines
- Architecture overview
- Code standards
- Pull request process

### 4. Search Functionality

The built docs include a search feature - try searching for "collocation" or "satellite" in the docs.

## Common Tasks

### Rebuild After Code Changes

When you update docstrings in your code:

```bash
cd docs
make html
```

The API docs will automatically update!

### Add a New Page

1. Create a new `.rst` file in `docs/source/`
2. Add it to the `toctree` in `index.rst` or relevant section
3. Rebuild with `make html`

### Update API Documentation

If you add new modules or restructure code:

```bash
cd docs
sphinx-apidoc -f -o source/api ../ocstrack
make html
```

### Check for Warnings

```bash
cd docs
make html 2>&1 | grep -i warning
```

Address warnings to improve documentation quality.

## Next Steps

### For Immediate Use

1. ✅ Documentation is ready to view locally
2. Review the generated pages and customize content
3. Fill in tutorial placeholders with real examples
4. Add more detailed explanations where needed

### For Production Deployment

When ready to deploy to ReadTheDocs:

1. Create `.readthedocs.yaml` in the repository root
2. Connect your GitHub repo to ReadTheDocs
3. Documentation will build automatically on every commit

### For Continuous Integration

Add documentation build to your GitHub Actions:

```yaml
# .github/workflows/docs.yml
name: Build Documentation

on: [push, pull_request]

jobs:
  docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - name: Install dependencies
        run: |
          pip install sphinx sphinx-rtd-theme sphinx-autodoc-typehints nbsphinx myst-parser
      - name: Build docs
        run: |
          cd docs
          make html
```

## Troubleshooting

### Issue: "make: command not found"

**Solution**: Use sphinx-build directly:

```bash
cd docs
sphinx-build -b html source build/html
```

### Issue: Import errors when building

**Solution**: The `autodoc_mock_imports` in `conf.py` should handle this, but if you still have issues:

```bash
# Install OCSTrack dependencies first
pip install -r requirements.txt
```

### Issue: Changes not appearing

**Solution**: Clean build:

```bash
cd docs
make clean
make html
```

### Issue: Broken internal links

**Solution**: Check that all referenced files exist and toctree entries are correct.

## Questions?

- Check the official Sphinx documentation: https://www.sphinx-doc.org/
- Read the Docs theme docs: https://sphinx-rtd-theme.readthedocs.io/
- OCSTrack issues: https://github.com/noaa-ocs-modeling/OCSTrack/issues

## Success!

Your documentation is now live locally. The build succeeded with minor warnings (mostly related to Python 3.6 type hints syntax).

**What you have now:**

- ✅ Professional documentation website
- ✅ Auto-generated API reference
- ✅ User guides and tutorials
- ✅ Search functionality
- ✅ Mobile-responsive design
- ✅ Accessibility features

**View it now at**: `docs/build/html/index.html`
