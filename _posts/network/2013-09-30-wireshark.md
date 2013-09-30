---
published: true
layout: post
category: network
tags: 
  - wireshark
  - capture
  - packet
---

# Wireshark

## Note

* wireshark 1.10+ need gtk3

## Get Source

    svn co http://anonsvn.wireshark.org/wireshark/trunk-1.8/ wireshark-1.8

## Prepare

* for Ubuntu

        sudo apt-get install bison flex libgtk2.0-dev libglib2.0-dev libpcap-dev automake autoconf

## Install

    sh autogen.sh
    ./configure
    make
    sudo make install
    sudo ldconfig -v