---
layout: post
title:  "Compile GNU Octave with ICC and MKL"
date:   2016-06-01 16:00:00 +0100
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
    
* Download the latest stable `Octave` from its [website](ftp://ftp.gnu.org/gnu/octave).

* Configure `Octave`:

    TODO
   
* Install `LaTeX` and configure `CLASS_PATHS`. `LaTeX` is a prerequisite.

        $ sudo apt-get install tex-live-full

    Inside `octave/`:

        $ export CLASSPATH=.:$CLASSPATH

* Make and install:

        $ make
        $ make install

I have tried with Ubuntu 14.04. ICC version needs to be 2016 Update 3 (Update 2 didn't work).

