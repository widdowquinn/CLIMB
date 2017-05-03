<img src="images/JHI_STRAP_Web.png" style="width: 150px; float: right;">

# README.md

This repository contains notes about setting up servers on `CLIMB`, the MRC cloud infrastructure for microbial bioinforamtics.

* [`CLIMB` homepage](http://www.climb.ac.uk/)


## Table of Contents

1. [Starting a server](#startup)
2. [Accessing a server](#access)
3. [Things to do when you start](#configure)
4. [`Galaxy`](#galaxy)


## Online Tutorials and Documentation

* [Accessing `CLIMB` and Setup](https://discourse.climb.ac.uk/t/accessing-climb-and-setup/172)


<a id="startup"></a>
## 1. Starting a server

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

<a id="access"></a>
## 2. Accessing the server

At the `Dashboard` - [`https://bryn.climb.ac.uk/`](https://bryn.climb.ac.uk/) - you will see your running servers. Each one has a clickable IP address.

* Click on the IP address for your server. This takes you to your server's GVL dashboard.
* The available services on your server are indicated, with status icons

**NOTE:** it can take some time for all the services to come up, when the server is first created.

<a id="configure"></a>
## 3. Things to do when you start

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

* Change directory to the cloned repository: `cd ~/CLIMB`
* To see what will be installed, use `less requirements.txt`
* `sudo pip install -r requirements.txt`

<a id="galaxy"></a>
## 4. `Galaxy`

### Set up `Galaxy` administrator account

`Galaxy` should have been started by `CloudMan` when the server started. To set yourself up as an administrator on `Galaxy`, follow the instructions below, from teh server GVL dashboard.

* Follow the access link to `Galaxy`
* Select `User - Register` from the `Galaxy` top menu bar
* Add yourself as a user
* Return to the server GVL dashboard
* Follow the access link to `CloudMan`
* Click on `Admin` (upper right corner)
* Add your email address in the `Set Galaxy admin users` field
* Refresh the page: you should see that your email address is now one of the current Galaxy admins

### Upload dataset to `Galaxy` shared data

From the `Analyze Data` page of `Galaxy`, while logged in to your account, follow the instructions below:

* Click on `Get Data -> Upload File`
* Click on the `Choose local file` button, and select the files you wish to upload
* Click on `Start`. The upload process will begin, and your history panel will be populated with files
* Rename and save the history (optional)

To put the uploaded files into a shared data folder:

* Click on `Shared Data -> Data Libraries`
* Create a new library, if necessary. Otherwise select an existing library
* Click on `Add datasets to current folder -> from History`
* Select the appropriate history, and the appropriate files, and click `Add`

