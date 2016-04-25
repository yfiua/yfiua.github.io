---
layout: post
title:  "Setting up High Performance Python Environment for Network Analysis"
date:   2016-04-25 16:00:00 +0100
comments: true
categories: tech
---

1. Use Intel compilers and MKL to compile `NumPy` and `SciPy`

* Install [Intel C++ and Fortran compilers](https://software.intel.com/en-us/intel-compilers) and [MKL](https://software.intel.com/en-us/intel-mkl), which are free for academic use. Sourse the environment scripts:

		$ source /*path-to-mkl*/bin/mklvars.sh intel64
		$ source /*path-to-compilers*/linux/bin/compilervars.sh -arch intel64

	Check with some commands:

		$ icc -v
		$ echo $LD_LIBRARY_PATH
    
* Checkout the latest stable `NumPy` and `SciPy` from their Git repositories.
    
* Inside `numpy/`, create a file named `site.cfg` and type in the following:
        
        [mkl]
        library_dirs = /*path-to-mkl*/lib/intel64/
        include_dirs = /*path-to-mkl*/include/
        mkl_libs = mkl_rt
        lapack_libs =

* In `numpy/numpy/distutils/intelccompiler.py`, modify `class IntelEM64TCCompiler` and match the code to something like this:

        cc_exe = 'icc -m64 -O3 -g -fPIC -fp-model strict -fomit-frame-pointer -openmp -xHost'
        #cc_args = '-fPIC'

* In `numpy/numpy/distutils/fcompiler/intel.py`, modify `class IntelEM64TFCompiler` and match the code to something like this:

		possible_executables = ['ifort']

		def get_flags(self):
			# Scipy test failures with -O2 or -O3
			return ['-O1 -g -xhost -openmp -fp-model strict -fPIC']
		def get_flags_opt(self):
  			return []

		def get_flags_arch(self):
			return []

* In `numpy/`, build and install `NumPy`:

		$ python setup.py build --compiler=intelem | tee build.log
		$ sudo -H python setup.py install | tee install.log

	For some reason, installing without `sudo` causes `f2py` not correctly configured. Test if the installisation was successful:

		$ python
		>>> import numpy
		>>> numpy.__version__()
		>>> numpy.__config__.show()
		>>> numpy.test()

* Now `NumPy` is ALREADY installed, let's build and install `SciPy`. Inside `scipy/`,

		$ python setup.py config --compiler=intelem --fcompiler=intelem build_clib --compiler=intelem --fcompiler=intelem build_ext --compiler=intelem --fcompiler=intelem | tee build.log
		$ python setup.py install --user

	Test if the installisation was successful:

		$ python
		>>> import scipy
		>>> scipy.__version__()
		>>> scipy.__config__.show()
		>>> scipy.test()


The `python-igraph` in Ubuntu's default repository is usually outdated. To install the newest one:

1. Install packages `pip`, `python-dev`, `libxml2-dev` and `zlib1g-dev`

   These packages are needed but not pre-installed in Ubuntu by default.

        $ sudo apt-get install -y pip python-dev libxml2-dev zlib1g-dev

2. Use `sudo` when installing `igraph`

   To avoid error `could not create '/usr/local/lib/python2.7/dist-packages/igraph': Permission denied`, use:
    
        $ sudo -H pip install python-igraph

3. I had to install `libfreetype6-dev` and `libxft-dev` in order to enable `matplotlib`

        $ sudo apt-get install libfreetype6-dev libxft-dev
        $ sudo -H pip install matplotlib

I have tried in both Ubuntu 14.04 and 15.04.

Benchmark:

On a server with 8 cores @ 2.9GHz
