## 1. Download and install Anaconda Python environment. 
Anaconda is a great Python package manager, which allows you to access all kinds of scientific packages easily with several lines of commands. You can download it from its official website
https://www.anaconda.com/products/individual

After the installation, open your `Terminal` (Mac) or `Anaconda Prompt` (Windows), you should notice that `(base)` will be shown at the beginning of the prompt. 
Run the following command to make sure that you are actually using the Python from Anaconda. 
```
python -c "import sys; print(sys.executable)"
```
It will output the path of python, something similar to this
```
C:\Users\zheng\Anaconda3\python.exe
```

## 2. Configure repositories for installing OpenMM
OpenMM is not officially maintained by Anaconda, therefore you have to add `conda-forge` repository with the following command.

```
conda config --append channels conda-forge
```
Then run the following command to show the repositories currently in use
```
conda config --show channels
```
It will output something like this. Make sure `conda-forge` is on the list and it's after `defaults`.
```
channels:
  - defaults
  - conda-forge
```

## 3. Install OpenMM and other packages
Now that the Python environment been setup, it's time to install OpenMM and its dependencies, with the following two commands
```
conda install numpy matplotlib jupyter openmm mdtraj nglview

jupyter-nbextension enable nglview --py --sys-prefix
```

The last step is to validate that OpenMM is successfully installed. Just execute the following command
```
python -m simtk.testInstallation
```
It will perform a small test simulation with OpenMM, and output something like this
```
OpenMM Version: 7.5
Git Revision: b49b82efb5a253a7c891ca084b3370e181de2ea3

There are 4 Platforms available:

1 Reference - Successfully computed forces
2 CPU - Successfully computed forces
3 CUDA - Error computing forces with CUDA platform
4 OpenCL - Successfully computed forces

Median difference in forces between platforms:

Reference vs. CPU: 6.30321e-06
Reference vs. OpenCL: 6.75475e-06
CPU vs. OpenCL: 7.99175e-07

All differences are within tolerance.
```
The output will be different based on your hardware and graphical drivers. However, make sure __at least one of the `CPU`, `CUDA` and `OpenCL`__ is listed and have successfully computed forces.