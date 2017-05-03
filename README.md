<img src="images/JHI_STRAP_Web.png" style="width: 150px; float: right;">
# README.md

This repository contains notes about setting up servers on `CLIMB`, the MRC cloud infrastructure for microbial bioinforamtics.

* [`CLIMB` homepage](http://www.climb.ac.uk/)


## Online Tutorials and Documentation

* [Accessing `CLIMB` and Setup](https://discourse.climb.ac.uk/t/accessing-climb-and-setup/172)

## Starting a server

### Genomics Virtual Laboratory Server

* Go to the `Dashboard` at [`https://bryn.climb.ac.uk/`](https://bryn.climb.ac.uk/)
* Select `Launch a Genomics Virtual Laboratory server`
* Enter a suitable server name
* Choose a server type:
  * `User server` has 4 cores and 32GB RAM, 120GB HDD
  * `Group server` has 8 cores and 64GB RAM, 120GB HDD
* Enter a new server password (this gets referred to as the `cluster password` elsewhere)
* Click on `Launch Server`

After a short pause, the new server will appear under the `Running servers at <LOCATION>` header, with a name, created date, flavour, status (this should be `active`, an IP address, and an `Options` drop-down.

* The `Options` drop-down allows you to start, stop, reboot, or terminate the server. 
* Terminating a server deletes it from `CLIMB`.

## Accessing the server

At the `Dashboard` - [`https://bryn.climb.ac.uk/`](https://bryn.climb.ac.uk/) - you will see your running servers. Each one has a clickable IP address.

* Click on the IP address for your server. This takes you to your server's GVL dashboard.
* The available services on your server are indicated, with status icons

**NOTE:** it can take some time for all the services to come up, when the server is first created.


## Things to do when you start

By default, the `user` servers install `Jupyterhub` and `RStudio`, but the `group` servers do not. These are GVL pacakages and can be installed as described below.

### Installing new GVL packages

* At the server's GVL dashboard, click on `Admin`
* You will be presented with a set of packages, each of which has a badge saying either `Installed` or `Install`
* Click on `Install` for the packages you require
* When installation is complete, the new packages should be available in the GVL dashboard for the server

### Fixing `Jupyterhub` 500 error

The GVL package installation of `Jupyterhub` does not work 'out of the box' and gives a 500 error when login is attempted. To fix this, follow the instructions below.

* SSH in to the server
* Issue the command: `sudo pip install --upgrade jupterhub`
* `Jupyterhub` should now work correctly

### Packages to upgrade/install

Having logged in to the server by SSH:

* Update `apt-get`: `sudo apt-get update`
* `Emacs`: `sudo apt-get install emacs`

### Clone this repository

* `git clone https://github.com/widdowquinn/CLIMB.git`

### Add `Python` packages

We want to make useful bioinformatics/scientific packages available to `Jupyterhub`. These can be installed with `pip`, using the `requirements.txt` from this repository.

* To see what will be installed, use `less requirements.txt`
* `sudo pip install -r requirements.txt`