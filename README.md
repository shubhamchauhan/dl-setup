# Guide to set up your Deep Learning Machine from Scratch
This file is a guide to setup your deep learning machine. It is not a comprehensive guide to deal with all the installation issues. I have made this to communicate the primary instructions to my team members. I've intentionally left out the Nvidia driver update,CUDA and cuDNN installation. For the time being lets build some baby networks to validate our models. After that we will move to more generalised datasets and distributed learning.

**Basics**

First, open a terminal and run the following commands to make sure your OS is up-to-date

    sudo apt-get update  
    sudo apt-get upgrade  
    sudo apt-get install build-essential  
    sudo apt-get autoremove 

    Install git

    sudo apt-get install git 

**Tensorflow**

This installs v0.8 without GPU support. Instructions below are from [here] (https://www.tensorflow.org/versions/r0.8/get_started/os_setup.html)

    sudo pip install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.8.0-cp27-none-linux_x86_64.whl

Run a test to ensure your Tensorflow installation is successful. When you execute the import command, there should be no warning/error.

    python
    >>> import tensorflow as tf
    >>> exit()

If the python is not able to import the library, add library path to the python environment. The path is case specific. Search in your system to find it out

    python
    >>> import sys
    >>> sys.path.append('/usr/local/lib/python2.7/dist-packages') 
    >>> sys.path.append('/usr/local/lib/python2.7')


**OpenBLAS**

OpenBLAS is a linear algebra library and is faster than Atlas. This step is optional, but note that some of the following steps assume that OpenBLAS is installed. You'll need to install gfortran to compile it.

    mkdir ~/git
    cd ~/git
    git clone https://github.com/xianyi/OpenBLAS.git
    cd OpenBLAS
    make FC=gfortran -j $(($(nproc) + 1))
    sudo make PREFIX=/usr/local install

Add the path to your LD_LIBRARY_PATH variable

    echo 'export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH' >> ~/.bashrc

**Common Tools**

    Install some common tools from the Scipy stack

    sudo apt-get install -y libfreetype6-dev libpng12-dev
    pip install -U matplotlib ipython[all] jupyter pandas scikit-image

**Theano**

Install the pre-requisites and install Theano. These instructions are sourced from here

    sudo apt-get install python-numpy python-scipy python-dev python-pip python-nose g++ python-pygments python-sphinx python-nose
    sudo pip install Theano

Test your Theano installation. There should be no warnings/errors when the import command is executed.

    python
    >>> import theano
    >>> exit()

**Keras**

Keras is a useful wrapper around Theano and Tensorflow. By default, it uses Theano as the backend. See here for instructions on how to change this to Tensorflow.

    sudo pip install keras

**X2Go**

If your deep learning machine is not your primary work desktop, it helps to be able to access it remotely. X2Go is a fantastic remote access solution. You can install the X2Go server on your Ubuntu machine using the instructions below.

    sudo apt-get install software-properties-common
    sudo add-apt-repository ppa:x2go/stable
    sudo apt-get update
    sudo apt-get install x2goserver x2goserver-xsession

X2Go does not support the Unity desktop environment (the default in Ubuntu). I have found XFCE to work pretty well. More details on the supported environmens here

    sudo apt-get update
    sudo apt-get install -y xfce4 xfce4-goodies xubuntu-desktop

Find the IP of your machine using

    hostname -I

You can install a client on your main machine to connect to your deep learning server using the above IP. More instructions here depending on your Client OS
