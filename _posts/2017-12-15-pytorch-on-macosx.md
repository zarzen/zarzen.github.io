---
layout: post
title:  "Install Pytorch with GPU support on High Sierra"
date:   2017-12-15 16:30:00
categories: pytorch macosx machine_learning
---
Disable SIP.

Install `cuda-8`. Though `cuda-9` released for High Sierra, `cudnn-7` is not available for `mac osx`. After installation upgrade `cuda driver` through `system preference` panel, as shown below. If not upgrade to newest `cuda driver` the compiled application cannot run on High Sierra. `cuda-8` only has `10.12` version, but it's fine.  

Download `cudnn-v6` for `mac osx` from [Nvidia cudnn](https://developer.nvidia.com/cudnn) and install it.

![CUDA panel]({{ "/assets/imgs/cuda_panel.png" | absolute_url}})
![Upgrade CUDA driver]({{ "/assets/imgs/cuda_upgrade.png" | absolute_url}})

Install `Xcode-8.2.x`, either `8.2` or `8.2.1` is fine, based on documents of `cuda-8.0.61`. Download `Xcode` from <a href="https://developer.apple.com/download/more/">Apple Developers Download Center</a>. We can install different versions of `Xcode`  by renaming `Xcode` to `Xcode_8_2`. Once we installed 

continuing...