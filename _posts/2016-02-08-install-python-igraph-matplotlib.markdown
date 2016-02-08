---
layout: post
title:  "Install python-igraph and matplotlib on Ubuntu"
date:   2016-02-08 16:00:00 +0100
comments: true
categories: tech
---

The `python-igraph` in Ubuntu's default repository is usually outdated. To install the newest one:

1. Install packages `pip`, `python-dev`, `libxml2-dev` and `zlib1g-dev`

   These packages are needed but not pre-installed in Ubuntu by default.

        $ sudo apt-get install -y pip python-dev libxml2-dev zlib1g-dev

2. Use `sudo` when installing `igraph`

   To avoid error `could not create '/usr/local/lib/python2.7/dist-packages/igraph': Permission denied`, use:
    
        $ sudo pip install igraph

3. I had to install `libfreetype6-dev` and `libxft-dev` in order to enable `matplotlib`

        $ sudo apt-get install libfreetype6-dev libxft-dev
        $ sudo pip install matplotlib

I have tried in both Ubuntu 14.04 and 15.04.
