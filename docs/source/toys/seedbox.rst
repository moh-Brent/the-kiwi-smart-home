Seedbox
=======

.. contents:: Table of Contents

The Setup
---------
Installed on ProxmoxVE
with Debian on the VM

Login to Debain VM

SETUP NETWORK DRIVES AND MOUNT
------------------------------

Setup NAS Drive Folders to Share

Create users with the correct UID and GID

Create Drives

Share Drives



3.2	AS PER INSTRUCTIONS IN NUC DOCS ADD DETAILS

3.3	HTPC CREATE AND MOUNT DRIVES 
--------------------------------
Login using “The_Login” account this is required as the folders on the NAS will be setup with “The_Login” UID and GID = 1000


Create the folders
------------------
Not sure you need to use sudo for these as I have changed this and it works
sudo mkdir /shares
sudo mkdir /shares/backup
sudo mkdir /shares/plex 
or
sudo mkdir /shares
mkdir /shares/backup
mkdir /shares/plex


Mount Drives at System Startup
------------------------------
Before mounting drives install the following utilities
sudo apt-get install cifs-utils nfs-common
If the error relates to setting up an sshfs mount, the sshfs package may be missing (fix with sudo apt install sshfs )

Backup FSTAB file
-----------------
sudo cp /etc/fstab /etc/fstab.backup
Now we can edit fstab:
sudo nano /etc/fstab
add the following
192.168.0.11:/data/plex /shares/plex nfs defaults 0 0
192.168.0.11:/data/backup /shares/backup nfs defaults 0 0
Ctrl X+Y Enter

Reboot
**sudo reboot**
log in and check that you can see all the files from your shared storage


4	DOCKER-CE

https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl

4.1	INSTALLING DOCKER
Should already be installed as per xxxxxxxxx
5	PORTAINER

5.1	INSTALL PORTAINER
Should already be installed as per xxxxxxxxx



6	DELUGE + OPENVPN


sudo docker pull sgtsquiggs/deluge-openvpn

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




7	JACKETT

Before we setup Sonarr and crew, lets start with Jackett. Similar to the command before, we need to edit the two '-v' lines:

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

8	OMBI


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


9	SONARR



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

sudo apt-get install apt-transport-https -y --force-yes

Connect to it using http://192.168.0.XXX:8989/ or whatever your IP address is.
9.1	CONFIGURE SONARR

10	RADARR

Command to edit and run:

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

11	LIDARR


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


12	ORGANIZR

https://github.com/causefx/Organizr

https://organizr.app/

https://docs.organizr.app/books/setup-features/page/sso

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



