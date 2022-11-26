---
layout: post
title:  "Tensorflow Tips"
date:   2017-08-26 20:18:31
categories: tensorflow
---

## Set visible GPU to `tensorflow`
``` python
import os
os.environ["CUDA_DEVICE_ORDER"] = "PCI_BUS_ID"
os.environ["CUDA_VISIBLE_DEVICES"] = "2"
```

## Set memory usage
``` python
gpu_options = tf.GPUOptions(per_process_gpu_memory_fraction=0.25)
sess = tf.Session(config=tf.ConfigProto(gpu_options=gpu_options))
```
