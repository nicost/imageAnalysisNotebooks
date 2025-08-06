# 2. Installing Jupyter with Napari using uv

## Goal of this tutorial
Python is an incredibly powerful environment for analysis of biological images.
Display of multi-dimensional images used to be difficult, but tools such as 
napari have made this much more approachable.  Running Python code interactively
in a Jupyter notebook is very comfortable and makes it easy to create 
scripts that do exactly what you would like them to be doing.  

One of the hurdles in working with Python lies in the need to maintain different environments for different projects (because the libraries/dependencies often clash with each other).  Several tools to manager Python environments (such as Python `venv`, and `anaconda` exist.  Recently the tool `uv` (which is written in the l;anguage Rust) has become popular because it is fast, reliable and efficient.  Here we will use `uv` to install an environment that can run Jupyer notebooks, display images from the notebook in napari and use and (nvidia) GPU if available.

## Install `uv`
Follow the [instructions](https://docs.astral.sh/uv/getting-started/installation/) for your platform. 

Confirm succesfull installation by typing `uv version` in a command terminal (such as powershell on windows or the terminal app on Mac OS).  The response should look like:

`uv 0.6.12 (e4e03833f 2025-04-02)`

## Creating the environment
First, you need to decide where to store your environments.  I tend to do this in a directory `projects` within my home directoyr, and within `projects` I make a directory `python-projects` (i.e. the windows path is `C:\Users\nstuurman\projects\python-projects`), but you are free to organize this differently. Once you have a place, go there in the terminal application (in Windows Powershell or the Mac terminal, you can type `cd` then drag the path from a File Explorer window into the terminal). 

Now create the virtual environment:
```
uv venv jupyter_napari --python=3.11
```

This created a directory called "jupyter_napari" and placed the files needed for a Python virtual environment in there.

Activate this environment with:
```
.\jupyter_napari\Scripts\activate.bat
```

Now you can install the needed packages into the virtual environment:
```
uv pip install jupyter
uv pip install napari[all]
```

Where glasbey provides a nice LUT (ColorMap) for segmented objects.


## Test the environment
On the command prompt type:
```
jupyter lab
```
If all goes well, your browser will open Jupyter and have a "Launcher" tab.  Click on "Python 3 (ipykernel).
```
%gui qt6
from skimage import data
import napari

viewer = napari.Viewer()
layer = viewer.add_image(data.moon())
```

## Add Cellpose
Cellpose uses deap learning networks for cell segmentation.  To add Cellpose to your environment:
```
 uv pip install cellpose[gui]
```
If you have a CUDA-capable GPU, you will get much better performance by using it.  To do so, you will first need to figure out if the NVIDIA driver for your GPU is installed, and have the correct pytorch cudatoolkit. To check if CUDA is installed, in the terminal type:
```
nvcc --version
```
Mine responds with:
```
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2022 NVIDIA Corporation
Built on Wed_Sep_21_10:41:10_Pacific_Daylight_Time_2022
Cuda compilation tools, release 11.8, V11.8.89
Build cuda_11.8.r11.8/compiler.31833905_0
```
which means that I have CUDA 11.8 installed.  If nvcc is not found, you will need to [install CUDA from the NVidia website](https://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html).  Regretfully, this can be daunting.  

Once you have CUDA installed, and know which version it is, you should install a compatible [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit-archive).  Cellpose currently advises to stick to the 11.x releases.



Now modify the pytorch installation that came with Cellpose to use the GPU:
```
uv pip uninstall torch
```

To install the GPU version of torch, follow the instructions [here](https://pytorch.org/get-started/locally/). The uv pip installs should work across platforms, you will need torch and torchvision, e.g. for windows + cuda 11.8 the command is

```
uv pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

Check that Cellpose uses the GPU:
```
python -m cellpose --version
```
I get the following response:
```
Welcome to CellposeSAM, cellpose v
cellpose version:       4.0.6
platform:               win32
python version:         3.11.11
torch version:          2.7.1+cu118! The neural network component of
CPSAM is much larger than in previous versions and CPU excution is slow.
We encourage users to use GPU/MPS if available.



cellpose version:       4.0.6
platform:               win32
python version:         3.11.11
torch version:          2.7.1+cu118
```
Indicating that Cellpose is using the cuda enhanced torch version.

Now start Jupyter:
```
jupyter lab
```
%gui qt5
from skimage import data
import napari
import numpy as np
from cellpose import models, io

# open viewer and show a skimage image
viewer = napari.Viewer()
image = data.human_mitosis()
layer = viewer.add_image(image)

# Use Cellpose to segment the image and show the masks in napari
# Load a pretrained model
model = models.CellposeModel(gpu=True)
# Define channels (e.g., [0,0] for single-channel grayscale)
channels = [0,0]
# Evaluate the image to get masks, flows, styles, and diameters
masks, flows, styles = model.eval(image, diameter=None)
# Show masks in napari as a new layer
layer2 = viewer.add_image(masks)




