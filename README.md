# xarm-dev for Ubuntu

xarm-dev is a package to set up Ubuntu to use the Python hidusb module in order to connect to the Lobot xArm. 
Installation of xarm-dev loads Ubuntu dependencies. It also includes a tool to initialize a Python development
environment and load Python dependencies. In other words, xarm-dev takes the work out of setting a Python development
environment for working with the xArm.

The following Ubuntu packages are loaded:

* python3
* python3-pip
* python3-venv
* python3-dev
* libusb-1.0-0-dev
* udev
* libudev-dev

Also installed is command xarm-dev.

usage: xarm-dev [--version] [--help] <command> <[args]>

xarm-dev commands:

**init:**

* Initialize a project folder. Activate a virtual Python environment, upgrade setuptools and install hidapi package into virtual environment site packages.

## xarm-dev init does the following:

* python3 -m venv env
* source env/bin/activate
* pip3 install --upgrade setuptools
* pip3 install hidapi

## Installation

    sudo apt install ./xarm-dev_0.1-ubuntu.deb

## Uninstall

Package dependencies must be manually unloaded or all can be unloaded using apt-get's autoremove option.

    sudo apt --purge remove xarm-dev

## Build

    dpkg-deb --build xarm-dev_0.1-ubuntu
