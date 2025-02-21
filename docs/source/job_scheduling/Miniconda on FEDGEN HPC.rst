Miniconda on FEDGEN HPC
=======================

We have a centralized installation of Miniconda on the FEDGEN HPC
Cluster. Miniconda is a free open source minimal installer for Conda. It
is a small, bootstrap version of Anaconda that includes only Conda,
Python, the packages they depend on, and a small number of other useful
packages, including pip, zlib and a few others.

Conda package manager
~~~~~~~~~~~~~~~~~~~~~

In addition to
the `Conda <https://en.wikipedia.org/wiki/Conda_(package_manager)>`__ package
manager, Miniconda provides a number of package management tools
including the familiar Python
ones: `pip <https://en.wikipedia.org/wiki/Pip_(package_manager)>`__ and `EasyInstall <https://en.wikipedia.org/wiki/Setuptools#EasyInstall>`__.

The conda cheat sheet gives you a list of useful commands in a
glance: `Conda-cheat-sheet <https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf>`__

conda is available as a module on the HPC Cluster.

Usage
-----

**Python distribution module file conflicts**

To prevent errors when running the Python interpreter, attempting to
load an additional Python distribution module after loading a Miniconda
module will produce a module load conflict error.

To run the default installed version of Miniconda (Python 3), simply
load the conda module:

*module load conda*

*You can then check your Python version:*

*$ which python*

*/share/apps/centos7/miniconda/X.Y.Z/bin/python*

*$ python -V*

*Python 3.X.Y*

You will see a confirmation message when the module is loaded.

Conda Environments
~~~~~~~~~~~~~~~~~~

Environments in conda are self-contained, isolated spaces where you can
install specific versions of software packages, including dependencies,
libraries, and Python versions. This isolation helps avoid conflicts
between package versions and ensures that your projects have the exact
libraries and tools they need.

Working with conda environments ensures isolation of dependencies,
reproducibility, Ease of management and development testing.

Some default environments have been created on FEDGEN HPC and
researchers should make request if they which to create other
environment.

Researchers can create other environments in their Home Space but We do
not recommend it.

.. _section-1:

**Listing environments**
^^^^^^^^^^^^^^^^^^^^^^^^

You can list existing Conda environments as follows:

*user@allot:~$ module load conda*

*user@allot:~$ conda env list*

*# conda environments:*

*#*

*base /fedgenapps/software/conda*

*biocode /fedgenapps/software/conda/envs/biocode*

*jupyterlab /fedgenapps/software/conda/envs/jupyterlab*

**Activating environments**

conda activate <environment name>

user@allot:~$ conda activate biocode

(biocode) feduser@allot:~$

**De-Activating Environments**

conda activate <environment name>

user@allot:~$ conda activate biocode

(biocode) feduser@allot:~$

**List Installed packages in an Environments**

The conda list command will show all of the packages installed into your
environment.

*(biocode) user@allot:~$ conda list*

*# packages in environment at /fedgenapps/software/conda/envs/biocode:*

*#*

*# Name Version Build Channel*

*\_libgcc_mutex 0.1 main*

*\_openmp_mutex 5.1 1_gnu*

*\_r-mutex 1.0.0 anacondar_1*

*\_sysroot_linux-64_curr_repodata_hack 3 haa98f57_10*

*binutils_impl_linux-64 2.40 h5293946_0*

*binutils_linux-64 2.40.0 hc2dff05_1*

*blas 1.0 openblas*

*bowtie 1.2.3 py37hc9558a2_0 bioconda*

*bwa 0.7.17 h5bf99c6_8 bioconda*

*bwidget 1.9.16 h9eba36c_0*

*bzip2 1.0.8 h5eee18b_6*

*─*

*(package list redacted)*

.. _section-2:

**In a Job Script**
^^^^^^^^^^^^^^^^^^^

To make sure that you are running in your project environment in a
submission script, make sure to include the following lines in your
submission script before running any other commands or scripts (but
after your Slurm directives):

#!/bin/bash#SBATCH --partition=debug

#SBATCH --job-name=my_conda_job

#SBATCH --cpus-per-task 4

#SBATCH --mem-per-cpu=6000

module load conda

conda activate env_name

python exampleapp.py
