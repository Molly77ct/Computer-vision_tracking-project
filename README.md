# DroneMOT Environment Setup and Initial Progress

## Overview

This project documents the setup of a development environment for executing 
a multi-object tracking model for drone imagery based on the DroneMOT and 
FairMOT frameworks.

The objective of this setup is to assess the robustness and reliability of
 a multi-object tracking model in forested areas, considering the challenges
 imposed by complex backgrounds, frequent occlusions, scale variations, and 
the simultaneous movement of the UAV and target objects.

To support this research, a Linux environment was configured using Windows 
Subsystem for Linux (WSL) on Windows 11, followed by the installation of
 the required libraries and dependencies for FairMOT and Deformable 
Convolutional Networks v2 (DCNv2).

The implementation builds upon the DroneMOT project, which adapts 
multi-object tracking methods to aerial drone imagery scenarios.

During the environment setup, ChatGPT was used as a technical assistant to
 troubleshoot dependency conflicts, installation issues, and library 
compatibility problems encountered while configuring CUDA, Python packages, 
and compiling required modules.

------------------------------------------------------------------------
## References

DroneMOT Repository  
https://github.com/PenK1nG/DroneMOT

FairMOT: On the Fairness of Detection and Re-Identification in 
Multiple Object Tracking  

https://github.com/ifzhang/FairMOT

DCNv2: Deformable Convolutional Networks v2  
https://github.com/ifzhang/DCNv2

OpenAI ChatGPT was used as a technical assistant to help resolve
 dependency conflicts and environment configuration issues.
------------------------------------------------------------------------

# System Environment Setup

## 1. Create Linux Environment with WSL (Windows 11)

Following the readme of the repository the development environment was 
created using Windows Subsystem for
Linux (WSL) to run Ubuntu.

Install WSL:

``` bash
wsl --install
```

After installation, Ubuntu was initialized and configured.

Verify WSL installation:

``` bash
wsl --status
```

------------------------------------------------------------------------

## 2. Install Python (Latest Version)

Ubuntu was updated and Python installed.

``` bash
sudo apt update
sudo apt upgrade
sudo apt install python3
```

Check installation:

``` bash
python3 --version
```

------------------------------------------------------------------------

## 3. Install Conda

To manage project dependencies and environments, Conda was installed.

Download Miniconda:

``` bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

Install:

``` bash
bash Miniconda3-latest-Linux-x86_64.sh
```

Restart terminal and verify:

``` bash
conda --version
```

------------------------------------------------------------------------

# DCNv2 Installation

The Deformable Convolutional Networks v2 (DCNv2) library is required by
FairMOT for improved object detection.

Repository: https://github.com/ifzhang/DCNv2/tree/pytorch_1.7

Clone the repository:

``` bash
git clone https://github.com/ifzhang/DCNv2.git
```

Create the conda environment:

``` bash
conda create -n dcnv2 python=3.8
conda activate dcnv2
```

Ubuntu already includes C++ compilers, therefore no additional
installation was required.

------------------------------------------------------------------------

# FairMOT Installation

FairMOT is used for joint object detection and re-identification, which
improves the fairness between both tasks in multi-object tracking.

Repository: https://github.com/ifzhang/FairMOT

Clone the project:

``` bash
git clone https://github.com/ifzhang/FairMOT.git
cd FairMOT
```

------------------------------------------------------------------------

# Install CUDA Toolkit

To enable GPU acceleration for deep learning models, NVIDIA CUDA Toolkit
was installed.

``` bash
sudo apt install nvidia-cuda-toolkit
```

Verify installation:

``` bash
nvcc --version
```

------------------------------------------------------------------------

# Install Python Dependencies

FairMOT includes a requirements.txt file with required libraries.

Install dependencies:

``` bash
pip install -r requirements.txt
```

Additionally, Cython is required for compiling some modules:

``` bash
pip install cython
```

------------------------------------------------------------------------

# Build Correlation Package

FairMOT requires compiling a correlation module used in the tracking
network.

Navigate to the directory:

``` bash
cd ./src/lib/models/networks/correlation_package
```

Compile the extension:

``` bash
python setup.py build_ext --inplace
```

This step builds the correlation layers required by the tracking model.

------------------------------------------------------------------------

# Current Project Status

At this stage, the following components have been successfully
configured:

✔ Ubuntu environment using WSL\
✔ Python and Conda environment management\
✔ DCNv2 installation\
✔ FairMOT repository setup\
✔ CUDA Toolkit installation\
✔ Python dependencies installation\
✔ Correlation package compilation

This environment enables the execution and experimentation with
multi-object tracking models for UAV imagery.

------------------------------------------------------------------------

# Next Steps

Future work in this project includes:

-   Running the DroneMOT/FairMOT tracking pipeline
-   Testing on UAV forested video
-   Evaluating tracking metrics such as:
    -   MOTA (Multiple Object Tracking Accuracy)
    -   MOTP (Multiple Object Tracking Precision)
    -   IDF1 (Identity F1 Score)
-   Investigating the impact of drone motion on tracking performance
