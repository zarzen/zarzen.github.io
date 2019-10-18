---
layout: post
title:  "Running Horovod on two nodes"
date:   2019-10-17
categories: machine_learning distributed_training 
---

# Install OpenMPI
If Open MPI is not available, Horovod can still be installed without error, Because it will use `gloo` as backend. While `gloo` has
some issues when no GPU is available or only one GPU is available. After the installation Open MPI you need to make sure Horovod is able to find it. Otherwise, it still compiles without Open MPI support.

Install MPI on with following commands:
```
# download and compile from source
wget https://download.open-mpi.org/release/open-mpi/v4.0/openmpi-4.0.2.tar.gz

gunzip -c openmpi-4.0.2.tar.gz | tar xf -
cd openmpi-4.0.2
./configure --prefix=/usr/local

make -j25 all
sudo make install

```

After installation run `sudo ldconfig` to refresh library loading paths.

# Install Horovod
Install Machine Learning frameworks like `tensorflow`, `pytorch` or `mxnet` first, so that Horovod will compile with corresponding supports.

```
pip install tensorflow
pip install torch torchvision
pip install mxnet
pip install mxnet-mkl

pip install horovod
```
In case installed horovod is not with open MPI support at first, you need to reinstall, after doing `sudo ldconfig`.
```
pip uninstall horovod

pip install --no-cache-dir horovod
```

# Running Horovod
First, we need to make sure all workers are configured with password-less login(using ssh-keys). Next, if you are going to run jobs on local, then using `localhost` instead of hostname of the local machine. It took me for a while to figure out why `mpirun` hangs there.
```
# running with horovodrun
horovodrun -np 4 \
    -H <another-host>:2,localhost:2 \ 
    python tensorflow_mnist.py

# running with mpirun
mpirun -np 2 \
    -H localhost:1,<another-host>:1 \
    -bind-to none -map-by slot \
    -x NCCL_DEBUG=INFO -x PATH \
    -x NCCL_SOCKET_IFNAME=^lo,docker0 \
    -mca pml ob1 -mca btl ^openib \
    -mca btl_tcp_if_exclude lo,docker0 \
    python tensorflow_mnist.py
```