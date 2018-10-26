# Deep learning server configurate IBM POWER8 (ppc64le)

Bring more value to your organization’s data by developing with an entirely new approach to problems: deep learning, machine learning, and artificial intelligence. Unlock hidden potential and patterns in data organically — without you having to know the patterns, networks, or be an algorithmic expert. IBM is making deep learning easier and more performant for you with an enterprise software distribution of the most popular open-frameworks, in PowerAI.

In this tutorial we show a step to step for install and configure a deep learning server in IBM POWER8.

## ibmcom/powerai
- [powerai](https://hub.docker.com/r/ibmcom/powerai/)


## Nvidia Docker for POWER8

### For docker installation

    sudo echo 'deb http://ftp.unicamp.br/pub/ppc64el/ubuntu/16_04/docker-17.06.1-ce-ppc64el/ xenial main' >> /etc/apt/sources.list
    sudo apt-get update && apt-get install docker-ce
    sudo usermod -aG docker your-username

### For Nvidia-docker installation

    git clone https://github.com/NVIDIA/nvidia-docker.git
    git checkout 1.0
    git fetch --all
    cd nvidia-docker
    make deb
    cd dist
    sudo dpkg -i nvidia-docker_1.0.0~rc.3-1_ppc64el.deb

### Pulling Nvidia Cuda 8.0 with CuDNN 6

    nvidia-docker pull nvidia/cuda-ppc64le:8.0-cudnn6-devel-ubuntu16.04
    #Creating a container
    nvidia-docker run --name DL -v /home/projects:/data -d nvidia/cuda-ppc64le:8.0-cudnn6-devel-ubuntu16.04 tail -f /dev/null
    #Accesing container bash
    nvidia-docker exec -ti DL bash

## Anaconda3 for POWER8

    wget https://repo.continuum.io/archive/Anaconda3-5.0.0-Linux-ppc64le.sh

    ./Anaconda3-5.0.0-Linux-ppc64le.sh

## Pytorch with Anaconda

    # https://developer.ibm.com/code/howtos/install-pytorch-on-power    
    # https://github.com/ppc64le/build-scripts/blob/master/pytorch/ubuntu_build_intructions.txt
    
    export CMAKE_PREFIX_PATH="$(dirname $(which conda))/../"
    conda install numpy pyyaml setuptools cmake cffi
    git clone --recursive https://github.com/pytorch/pytorch
    cd pytorch
    python setup.py install

## Pytorch vision

    git clone https://github.com/pytorch/vision.git    
    cd vision    
    python setup.py install

## OpenCV for Power 8

    wget https://repo.continuum.io/pkgs/free/linux-ppc64le/opencv-3.1.0-np112py36_2.tar.bz2
    mkdir opencv-3.1.0-py36
    cd opencv-3.1.0-py36
    tar -jxvf ../opencv-3.1.0-np112py36_2.tar.bz2
    export PYTHONPATH=$PYTHONPATH:/home/<your-username>/opencv-3.1.0-py36/lib/python3.6/site-packages


## [PowerAI](http://ibm.biz/poweraideveloper) release 4 provides software packages for several Deep Learning frameworks and tools

https://public.dhe.ibm.com/software/server/POWER/Linux/mldl/ubuntu/README.html


- Bazel
- Caffe - BVLC, IBM, and NVIDIA variants
- Chainer
- DIGITS
- NCCL
- OpenBLAS
- OpenMPI - with CUDA enablement
- TensorFlow
- Theano
- Torch


## Blogs 

- https://developer.ibm.com/code/howtos/install-pytorch-on-power
- https://www.ibm.com/us-en/
- https://www.ibm.com/developerworks/community/blogs/fe313521-2e95-46f2-817d-44a4f27eba32/entry/Using_a_GPU_in_a_Docker_Container_on_POWER?lang=en
- https://www.ibm.com/developerworks/community/blogs/fe313521-2e95-46f2-817d-44a4f27eba32/entry/Building_Torch_on_OpenPOWER_Linux_Systems?lang=en
- https://www.ibm.com/developerworks/community/blogs/fe313521-2e95-46f2-817d-44a4f27eba32/entry/Building_DIGITS_on_OpenPOWER_Linux_Systems?lang=en
- https://www.ibm.com/developerworks/community/blogs/fe313521-2e95-46f2-817d-44a4f27eba32/entry/Building_TensorFlow_on_OpenPOWER_Linux_Systems?lang=en
- https://www.ibm.com/developerworks/community/blogs/fe313521-2e95-46f2-817d-44a4f27eba32/entry/Building_Caffe_on_OpenPOWER_Systems?lang=en
