---
layout: post
title:  "Install Pytorch with GPU support on High Sierra"
date:   2017-12-15 16:30:00
categories: pytorch macosx machine_learning
---
- !! Outdated: nvidia does not released `cudnn7.1` for macosx
- Disable SIP.

- Install `cuda-8`. Though `cuda-9` released for High Sierra, `cudnn-7` is not available for `mac osx`. After installation upgrade `cuda driver` through `system preference` panel, as shown below. If not upgrade to newest `cuda driver` the compiled application cannot run on High Sierra. `cuda-8` only has `10.12` version, but it's fine.  
![CUDA panel](/imgs/cuda_panel.png)

![Upgrade CUDA driver](/imgs/cuda_upgrade.png)

- Download `cudnn-v6` for `mac osx` from [Nvidia cudnn](https://developer.nvidia.com/cudnn) and install it.

- Install `Xcode-8.2.x`, either `8.2` or `8.2.1` is fine, based on documents of `cuda-8.0.61`. Download `Xcode` from <a href="https://developer.apple.com/download/more/">Apple Developers Download Center</a>. We can install different versions of `Xcode`  by renaming `Xcode` to `Xcode_8_2`. Once installed, select right version for Command Line Tools, by preference panel of Xcode as shown in following. 
![Choose CLT](/imgs/choose_CLT_version.png)

- Config environment variables in `.zshrc` or `.bash_profile` or other shell configurations. Add following content:
``` bash
export DYLD_LIBRARY_PATH=/usr/local/cuda/lib:$DYLD_LIBRARY_PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
```

- Make sure `anaconda` has installed and upgraded needed packages. 
``` bash
conda install numpy pyyaml setuptools cmake cffi # provided by pytorch README
# I remember some packages need newest version of mkl which is 2018-01, but default mkl in anaconda is mkl2017
conda upgrade mkl 
``` 

- Start compiling (last command is optional):    
``` bash
export CMAKE_PREFIX_PATH=[anaconda root directory] # temporal env variable
# get source code
# following command will get newest pytorch v0.4.0
git clone --recursive https://github.com/pytorch/pytorch
cd pytorch
# make and install
# it is fine using target 10.9; 
MACOSX_DEPLOYMENT_TARGET=10.9 CC=clang CXX=clang++ python setup.py install
# Optional !!!!!! if it failed before; do clean first
MACOSX_DEPLOYMENT_TARGET=10.9 CC=clang CXX=clang++ python setup.py clean 
```    
