# QuickAnnotator
---
Quick Annotator is an open-source digital pathology annotation tool.

![QA user interface screenshot](https://github.com/choosehappy/QuickAnnotator/wiki/images/Annotation_Page_LayerSwitch.gif)

# Purpose
---
Machine learning approaches for segmentation of histologic primitives (e.g., cell nuclei) in digital 
pathology (DP) Whole Slide Images (WSI) require large numbers of exemplars. Unfortunately, annotating 
each object is laborious and often intractable even in moderately sized cohorts. 
The purpose of the quick annotator is to rapidly bootstrap annotation creation for digital
pathology projects by helping identify images and small regions.

Because the classifier is likely to struggle by intentionally focusing in these areas, 
less pixel level annotations are needed, which significantly improves the efficiency of the users.
Our approach involves updating a u-net model while the user provides annotations, so the model is
then in real time used to produce. This allows the user to either accept or modify regions of the 
prediction.

# Requirements
---
Tested with Python 3.8

Requires:
1. Python 
2. pip

And the following additional python package:
1. Flask_SQLAlchemy
2. scikit_image
3. scikit_learn
4. opencv_python_headless
5. scipy
6. requests
7. SQLAlchemy
8. torch
9. torchvision
10.Flask_Restless
11. numpy
12. Flask
13. umap_learn
14. Pillow
15. tensorboardX
16. ttach
17. albumentations
18. config

You can likely install the python requirements using something like (note python 3+ requirement):
```
pip3 install -r requirements.txt
```
The library versions have been pegged to the current validated ones. 
Later versions are likely to work but may not allow for cross-site/version reproducibility

We received some feedback that users could installed *torch*. Here, we provide a detailed guide to install
*Torch*
### Torch's Installation
The general guides for installing Pytorch can be summarized as following:
1. Check your NVIDIA GPU Compute Capability @ *https://developer.nvidia.com/cuda-gpus* 
2. Download CUDA Toolkit @ *https://developer.nvidia.com/cuda-downloads* 
3. Install PyTorch command can be found @ *https://pytorch.org/get-started/locally/* 

### Docker requirements
Docker is a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers. Containers are isolated from one another and bundle their own software, libraries and configuration files.

In order to use Docker version of QA, user needs:
1. Nvidia driver supporting cuda. See documentation, [here](https://docs.nvidia.com/deploy/cuda-compatibility/index.html).
2. Docker Engine. See documentation, [here](https://docs.docker.com/engine/install/)
3. Nvidia-docker https://github.com/NVIDIA/nvidia-docker

PS: [Docker Desktop](https://github.com/choosehappy/QuickAnnotator/wiki/Frequently-Asked-Questions#how-to-install-docker-desktop) is an easy-to-install application for your Mac or Windows environment that enables you to build and share containerized applications and microservices. Docker Desktop includes Docker Engine, Docker CLI client, Docker Compose, Notary, Kubernetes, and Credential Helper.

Depending on your cuda version, we provide Dockerfiles for *cuda_10* and *cuda_11*.

To start the server, run either:
`docker build -t quick_annotator -f cuda_10/Dockerfile .` 
or 
`docker build -t quick_annotator -f cuda_11/Dockerfile .` 

from the *QuickAnnotator* folder.

When the docker image is done building, it can be run by typing:

`docker run --gpus all -p 5555:5555 quick_annotator`

*Note:* This command will forward port 5555 from the computer to port 5555 of the container, where our flask server is running as specificied in the [config.ini](https://github.com/choosehappy/QuickAnnotator/blob/main/config/config.ini#L6). It is critical that these numbers match in 3 places (2 on the command line and one in the config.ini). If this port is occupied on your machine, for example by another user or process, you will need to change both the value in the config.ini, rebuild the docker container, and then use the same value in the docker run command.

# Basic Usage
---
see [UserManual](https://github.com/choosehappy/QuickAnnotator/wiki/User-Manual) for a demo
### Run
```
 E:\Study\Research\QA\qqqqq\test1\quick_annotator>python QA.py
```
By default, it will start up on *localhost:5555*. Note that *5555* is the port number setting in [config.ini](https://github.com/choosehappy/QuickAnnotator/blob/main/config/config.ini#L6) and user should confirm {port number} is not pre-occupied by other users on the host. 

*Warning*: virtualenv will not work with paths that have spaces in them, so make sure the entire path to `env/` is free of spaces.
### Config Sections
There are many modular functions in QA whose behaviors could be adjusted by hyper-parameters. These hyper-parameters can 
be set in the *config.ini* file
- [common]
- [flask]
- [cuda]
- [sqlalchemy]
- [pooling]
- [train_ae]
- [train_tl]
- [make_patches]
- [make_embed]
- [get_prediction]
- [frontend]
- [superpixel]


# Advanced Usage
---
See [wiki](https://github.com/choosehappy/QuickAnnotator/wiki)

# Citation
---
Read the related paper on arXiv: [Quick Annotator: an open-source digital pathology based rapid image annotation tool](https://arxiv.org/abs/2101.02183)

PDF file available for [download](https://arxiv.org/ftp/arxiv/papers/2101/2101.02183.pdf)

Please use below to cite this paper if you find this repository useful or if you use the software shared here in your research.
```
  @misc{miao2021quick,
      title={Quick Annotator: an open-source digital pathology based rapid image annotation tool}, 
      author={Runtian Miao and Robert Toth and Yu Zhou and Anant Madabhushi and Andrew Janowczyk},
      year={2021},
      eprint={2101.02183},
      archivePrefix={arXiv},
      primaryClass={eess.IV}
  }
```
# Frequently Asked Questions
See [FAQ](https://github.com/choosehappy/QuickAnnotator/wiki/Frequently-Asked-Questions)




