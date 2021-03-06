---
layout: post
title:  Preparing your Raspberry Pi for University life
date:   2021-03-05 13:32:20 +0200
description: Getting your Raspberry Pi ready for science.
image: assets/images/raspberry-pi.jpg
tags: [Science, Open Hardware, Raspberry Pi]
categories: projects
author: mikkel
---

**The Raspberry Pi is an amazing little thing. It's a cheap small desktop computer AND it's a microcontroller, making it brilliant as both an experimental device, for programming and writing, as well as light data analysis. With different editions such as 4B, Zero WH and 400, they are tailored for the different needs. In other words, it's the ideal lab-mate.**

However, there's a few steps to make the Pi ideal for the university. Here's a brief tutorial:

# Accessing eduroam: Install Network Manager
Using eduroam for getting online is unfortunately not as straightforward as one could hope (see here). But luckily there is a simple way around that: Installing Network Manager - and it only requires a few steps.

___

First, we always start out updating and upgrading, and because outdated versions of `pip` and `setuptools` sometimes cause errors we'll upgrade those straight away too.

```zsh
sudo apt update && sudo apt upgrade
python3 -m pip install --upgrade pip setuptools
``` 
Next, we install Network Manager with all the necessary dependencies.
```zsh
sudo apt install network-manager network-manager-gnome openvpn \
openvpn-systemd-resolved network-manager-openvpn \
network-manager-openvpn-gnome
``` 

...before removing unnecessary libraries
```zsh
sudo apt purge openresolv dhcpcd5
```

# Install PsychoPy
## Enable OpenGL driver
sudo raspi-config 
> 6 Advanced options
> A2 GL Driver
> G2 GL (Fake KMS)

## Install PyQt5
sudo apt-get install qt5-default pyqt5-dev pyqt5-dev-tools
sudo apt install libgtk-3-dev

## Install psychopy
python3 -m pip install psychopy==3.2.4

## Install wxPython
python3 -m pip install wxPython

## Extra Psychtoolbox stuff (optional)
sudo apt-get install libusb-1.0.0-dev portaudio19-dev libasound2-dev
python3 -m pip install psychtoolbox

## Small NumPy fix
sudo apt-get install libatlas-base-dev

# Install HyperPixel4 software
curl https://get.pimoroni.com/hyperpixel4 | bash





# Install Python 3.9 and makee it default (optional)
## First install dependencies
sudo apt-get update
sudo apt-get install -y build-essential tk-dev libncurses5-dev libncursesw5-dev libreadline6-dev libdb5.3-dev libgdbm-dev libsqlite3-dev libssl-dev libbz2-dev libexpat1-dev liblzma-dev zlib1g-dev libffi-dev

## Compile
wget https://www.python.org/ftp/python/3.8.5/Python-3.8.5.tar.xz
tar xf Python-3.8.5.tar.xz
cd Python-3.8.5
./configure --prefix=/usr/local/opt/python-3.8.5
make -j 4

## Install
sudo make altinstall

## Remove files
cd ..
sudo rm -r Python-3.8.5
rm Python-3.8.5.tar.xz
. ~/.bashrc

## Make Python 3.8 default
`sudo update-alternatives --config python

## Verify
`python -V`

# Install virtualenv