*******
Seedbox
*******

.. contents:: Table of Contents

The Setup
---------
I have Proxmox setup on my server with a few Virtual Machines.
One of them is my Seedbox, I won't go into the setup of Proxcmox and the VM but you can look ast my basic tutorial here.

I'm using Debian as my OS of choice and I have a User and Password that is setup (standardised) across my devices, unfortunately I have to do that nmanually as I do not have a centralised login server.  Overkill for my and just about everyones home networks.

Login to Debain VM or use PuTTy https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html to get access to the OS.

Install Docker
--------------
Docker will hold all the apps that we will need to use for the Seedbox.

Setup Network Drives and Mount
------------------------------

NAS Folders and Share
=====================
Setup NAS Drive Folders to Share

Create users with the correct UID and GID

Create Drives

Share Drives



AS PER INSTRUCTIONS IN NUC DOCS ADD DETAILS

Create and Mount Drives on your OS
==============================
Login using “The_Login” account this is required as the folders on the NAS will be setup with “The_Login” UID and GID = 1000


Create the Folders
==================
Not sure you need to use sudo for these as I have changed this and it works

.. code-block:: bash

	sudo mkdir /shares
	sudo mkdir /shares/backup
	sudo mkdir /shares/plex 

or

.. code-block:: bash

	sudo mkdir /shares
	mkdir /shares/backup
	mkdir /shares/plex


Mount Drives at System Startup
------------------------------
Before mounting drives install the following utilities

.. code-block:: bash
	sudo apt-get install cifs-utils nfs-common
	
If the error relates to setting up an sshfs mount, the sshfs package may be missing , install using the below.

.. code-block:: bash

	sudo apt install sshfs )

Backup FSTAB file
-----------------
.. code-block:: bash
	
	sudo cp /etc/fstab /etc/fstab.backup

Now we can edit fstab:

.. code-block:: bash

	sudo nano /etc/fstab

add the following

.. code-block:: bash

	192.168.0.XXX:/data/plex /shares/plex nfs defaults 0 0
	192.168.0.XXX:/data/backup /shares/backup nfs defaults 0 0

Ctrl X+Y Enter


Reboot

.. code-block:: bash
   
	sudo reboot

log in and check that you can see all the files from your shared storage


DOCKER-CE
=========

https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl

INSTALLING DOCKER
-----------------

Should already be installed as per xxxxxxxxx

PORTAINER
=========

INSTALL PORTAINER
-----------------

Should already be installed as per xxxxxxxxx


DELUGE + OPENVPN
================

.. code-block:: bash
   
	sudo docker pull sgtsquiggs/deluge-openvpn

.. code-block:: bash
   
	sudo docker run --cap-add=NET_ADMIN --device=/dev/net/tun -d \
		      --name=deluge_openvpn \
		      --restart unless-stopped \
		      -v /shares/seedbox/deluge/config/:/config \
		      -v /shares/seedbox/downloads/:/downloads \
				  -v /shares/plex/completed/:/completed \
		      -v /etc/localtime:/etc/localtime:ro \
		      -e CREATE_TUN_DEVICE=true \
		      -e PUID=1000 \
		      -e PGID=1000 \
		      -e UMASK_SET=0 \
		      -e TZ=Pacific/Auckland \
		      -e OPENVPN_PROVIDER=[OpenVPN_Provider] \
		      -e OPENVPN_USERNAME=[OpenVPN_Username] \
		      -e OPENVPN_PASSWORD=[OpenVPN_Password] \
		      -e LOCAL_NETWORK=192.168.0.0/24 \
		      -p 8112:8112 \
		      -p 58846:58846 \
		      -p 58946:58946 \
		      -p 58946:58946/udp \
		      --dns 8.8.8.8 \
		      --dns 8.8.4.4 \
		      --dns 1.1.1.1 \
		      sgtsquiggs/deluge-openvpn




JACKETT
=======

Before we setup Sonarr and crew, lets start with Jackett. Similar to the command before, we need to edit the two '-v' lines:

.. code-block:: bash
   
	sudo docker create \
	  --name=jackett \
	  --restart unless-stopped \
	  -e PUID=1000 \
	  -e PGID=1000 \
	  -e TZ=Pacific/Auckland \
	  -p 9117:9117 \
	  -v /shares/seedbox/:/config \
	  -v /shares/seedbox/downloads:/downloads \
	  --restart unless-stopped \
	  linuxserver/jackett


http://192.168.0.XXX:9117/UI/Dashboard 

OMBI
====

.. code-block:: bash
   
	sudo docker create \
	  --name=ombi \
	  --restart unless-stopped \
	  -e PUID=1000 \
	  -e PGID=1000 \
	  -e TZ=Pacific/Auckland \
	  -p 3579:3579 \
	  -v /shares/seedbox/ombi:/config \
	  --restart unless-stopped \
	  linuxserver/ombi


http://192.168.0.XXX:3579 


SONARR
======

.. code-block:: bash

	sudo docker create \
	  --name=sonarr \
	  --restart unless-stopped \
	  -e PUID=1000 \
	  -e PGID=1000 \
	  -e TZ=Pacific/Auckland \
	  -p 8989:8989 \
	  -v /shares/seedbox/sonarr:/config \
	  -v /shares/plex/mytv:/mytv \
	  -v /shares/seedbox/downloads:/downloads \
	  --restart unless-stopped \
	  linuxserver/sonarr

Enable apt-get to install from https sources or you will get this error

The method driver /usr/lib/apt/methods/https could not be found.
To solve it install the https package

.. code-block:: bash
   
	sudo apt-get install apt-transport-https -y --force-yes

Connect to it using http://192.168.0.XXX:8989/ or whatever your IP address is.

CONFIGURE SONARR
----------------

RADARR
======

Command to edit and run:

.. code-block:: bash
   
	sudo docker create \
	  --name=radarr \
	  -e PUID=1000 \
	  -e PGID=1000 \
	  -e TZ=Pacific/Auckland \
	  -p 7878:7878 \
	  -v /shares/seedbox/radarr:/config \
	  -v /shares/plex/mymovies:/mymovies \
	  -v /shares/seedbox/downloads:/downloads \
	  --restart unless-stopped \
	  linuxserver/radarr


http://192.168.0.XXX:7878

LIDARR
======
.. code-block:: bash
   
	sudo docker create \
	  --name=lidarr \
	  -e PUID=1000 \
	  -e PGID=1000 \
	  -e TZ=Pacific/Auckland \
	  -p 8686:8686 \
	  -v /shares/seedbox/lidarr:/config \
	  -v /shares/plex/mymusic:/mymusic \
	  -v /shares/seedbox/downloads:/downloads \
	  --restart unless-stopped \
	  linuxserver/lidarr

http://192.168.0.XXX:8686


ORGANIZR
========

https://github.com/causefx/Organizr

https://organizr.app/

https://docs.organizr.app/books/setup-features/page/sso
.. code-block:: bash
	sudo docker create \
	  --name=organizr \
	  -v /shares/seedbox/organizr/config:/config \
	  -e PGID=1000 \
	  -e PUID=1000 \
	  -p 8081:80 \
	  organizr/organizr

http://192.168.0.XXX:8081

hash Key: [your_hash_key]

Registration Password: [reg_password]



