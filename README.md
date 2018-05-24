intensity-normalization
=====

This package contains code to normalize the intensity of various contrasts of MR neuro images

Requirements
------------

The number of dependencies in this project is, unfortunately, large. However, we have provided a script to
create a conda environment with the necessary packages (see create_env.sh, 
note that this takes some time to run since some packages need to be built from source).

The python requirements 

- Numpy
- Matplotlib
- nibabel
- scikit-learn
- scikit-fuzzy
- rpy2
- antspy

Furthermore, R needs to be installed with the following packages (and their dependencies):

- RAVEL
- WhiteStripe
- neurobase

For additional functionality, in R, also install 

- robex

Basic Usage
-----------

Install from the source directory

    python setup.py install
    
or (if you actively want to make changes to the package)

    python setup.py develop

and use the several provided command line scripts to interface with the package,
e.g., 

    ravel-normalize -i t1/ -m masks/ -o test_ravel --register -vv 

Project Structure
-----------------
```
intensity_normalization
│
└───intensity_normalization (source code)
│   │   errors.py (project specific exceptions)
│   │   
│   └───exec (holds executables)
│   │   │   fcm-normalize (call fuzzy c-means WM normalization on an directory)
│   │   │   gmm-normalize (call GMM WM normalization on an directory)
│   │   │   kde-normalize (call KDE WM normalization on an directory)
│   │   │   hm-normalize (call N&U HM intensity normalization on an directory)
│   │   │   ws-normalize (call WhiteStripe WM normalization on an directory)
│   │   │   ravel-normalize (call RAVEL intensity normalization on an directory)
│   │   │   robex (create brain masks for directory of images w/ ROBEX)
│   │   │   preprocess (resample, reorient, and bias field correct dir of imgs)
│   │   │   plot-hists (CLI to plot histograms for a directory)
│   │   │   tissue-mask (CLI to create tissue masks (i.e., CSF/GM/WM for a directory)
│   │   
│   └───normalize (modules for doing the actual intensity normalization)
│   │   │   fcm (use fuzzy c-means method for WM normalization)
│   │   │   gmm (use gaussian mixture model method for WM normalization)
│   │   │   kde (use kernel density estimate method for WM normalization)
│   │   │   hm (use Nyul & Udapa method for intensity normalization)
│   │   │   ws (use WhiteStripe method for WM normalization)
│   │   │   ravel (use RAVEL method for intensity normalization)
│   │
│   └───plot (modules for visualizing results of normalization)
│   │   |   hists (functions to plot histograms for all nifti images in a directory)
│   │   
│   └───utilities (functions not explicitly part of any particular intensity normalization routine)
│
└───tests (unit tests)
│   
└───docs (documentation)
```

Test Package
------------

Unit tests can be run from the main directory as follows:

    nosetests -v --with-coverage --cover-tests --cover-package=intensity_normalization tests
