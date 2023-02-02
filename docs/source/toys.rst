Toys
===============================================



RetroPie
Play Retro Games with Raspberry Pi RetroPie
In this Raspberry Pi RetroPie tutorial, we will show you how to install the popular RetroPie distribution to your Raspberry Pi and turn it into a retro gaming machine.
 

Using RetroPie, you can quickly turn your Raspberry Pi into a highly versatile retro gaming rig that is more than capable of running games for several systems such as the SNES, GBA, PS1, DOS and many more.
We will be showing you the process of installing and configuring RetroPie on your Raspberry Pi as well as how to copy roms to your Pi or connect it to a network drive.
For those who do not know what RetroPie is, it is a software package that is built on top of the Raspbian operating system. The package contains a range of different software that will enable the ability to emulate and play classic games.
RetroPie makes use of EmulationStation as its visual front end and uses the RetroArch project and various other emulator projects to emulate your games.
There are other emulator software packages that you can use instead of RetroPie. Be sure to check them out if you’re feeling adventurous.
Equipment
Below is all the equipment that you will need for setting up RetroPie on your Raspberry Pi.
Recommended
•	Raspberry Pi
•	Micro SD Card
•	USB Keyboard
•	USB Mouse
•	HDMI Cable
•	Monitor
Optional
•	Retro USB Controllers or Joysticks
•	Xbox Controller
•	PlayStation Controller
•	Ethernet Cable or Wi-Fi
Video
In this video guide, we walk you through the process of installing, setting up, and running a retro game using the RetroPie emulator package.
Below we have included a more in-depth guide on setting up RetroPie step by step.
How to setup Raspberry Pi RetroPie
Learn how to setup and run RetroPie on the Raspberry Pi
0 seconds of 6 minutes, 15 secondsVolume 90%
 
Adblock removing the video? Support us by subscribing to our ad-free service.
Installing RetroPie from Image
1. The first thing we need to do is obtain a copy of the RetroPie image for the Raspberry Pi.
You can find the available pre-built RetroPie images from the official RetroPie GitHub repository.
On this page, you should see the latest available release with a few download links near the bottom of the page. You will need to select the right image for your Raspberry Pi.
If you are using a Raspberry Pi 1 or a Raspberry Pi Zero, then download the “rpi1_zero.img.gz” file.
If you are using a Raspberry Pi 3 or newer, then download the “rpi2_rpi3.img.gz” file.
This image is a pre-built version of Raspbian Stretch that has RetroPie already set up on it and is one of the easiest ways to get the emulators running on your Raspberry Pi quickly.
If you would prefer you can setup RetroPie on your current installation, but we will go into those steps in another section.
2. Now that we have the RetroPie image, we will need to write the image to an SD Card that we are going to use with the Raspberry Pi.
To do this, we will be making use of a tool called “Etcher“. This tool will format the SD card and write the RetroPie image to it.
You can download Etcher by going to Etcher’s official website.
Once downloaded, install, and open the Etcher software.
3. With the Etcher software open, and the SD card connected to your computer, you can now start the process of writing the RetroPie image to it.
To begin this process click the “Select Image” button as shown below. In the dialog box that appears, find and select the RetroPie image that you previously downloaded.
 
4. With the RetroPie image selected, now go ahead and click the “Select drive” button.
This button will bring up a dialog asking you to select the drive that you would like to write the RetroPie image.
Make sure the one you choose is, in fact, your SD card as it will erase all data on that drive.
 
5. Now with the right image selected and the correct drive selected, you can now proceed to flash the SD Card by clicking the “Flash!” button.
 
Installing RetroPie from Scratch
If you decide that you would like to install RetroPie from scratch and not use the prebuilt image provided by the RetroPie team, then you can follow the instructions below.
Please note that it is recommended to use the prebuilt image as it comes with several things already setup and configured. You are also less likely to run into configuration issues from the beginning.
1. Before you begin, we will need to ensure that we have at least 2GB free on the Raspberry Pi’s SD Card for the RetroPie software to be able to install everything it needs.
If you are unsure if you have enough free space available on your Raspberry Pi’s SD Card, you can go ahead and use the following command.
df -hCopy
Below is an example of the output provided by the df -h command.
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        59G  1.6G   55G   3% /
You need to pay attention to the “/dev/root” filesystem, and the amount of space available under the “avail” column. As long as this is greater than “2G” you are free to proceed with installing RetroPie.
2. Now before we go ahead and install the RetroPie software package, we should first ensure that our Raspberry Pi is running up to date software.
We can achieve this by running the following two commands on the Raspberry Pi.
sudo apt-get update
sudo apt-get dist-upgradeCopy
We use the “dist-upgrade” command instead of the usual “upgrade” command as it ensures packages are updated to their latest version and will install new packages required by an upgrade.
3. With the Raspberry Pi’s operating system now up to date, we can now install the packages that the RetroPie setup script requires to operate.
One of the packages we need is the “dialog” package which is used by the RetroPie software script to build shell script dialog boxes.
The other package we need is the “git” package. We use this package to clone the setup script repository to our Raspberry Pi.
Install both of these packages by running the command below.
sudo apt-get install -y git dialogCopy
4. Now that we have installed all the packages that we need, we now go ahead and use the git software to clone the RetroPie setup script.
Enter the following two commands to clone the RetroPie setup script to your Raspberry Pi users home directory.
cd
git clone --depth=1 https://github.com/RetroPie/RetroPie-Setup.gitCopy
5. We can now change directory to the “RetroPie-setup” folder. This folder was created when we cloned the RetroPie setup script repository in the previous step.
After we change into the directory, we can go ahead and run the actual RetroPie setup script.
This script will run through the process of installing all packages required for the EmulationStation software as well as a few basic emulators.
You can do all of this by running the following two commands on your Raspberry Pi.
cd RetroPie-Setup
sudo ./retropie_setup.shCopy
6. You should now be seeing the RetroPie setup dialog on your display.
This dialog has a variety of different options, but the one we want to pay attention to is the “Basic Install” option. This option will be used to install all the “core” and “main” packages of RetroPie.
Select this option by using the arrow keys to navigate to it and using the enter button to select it.
 
7. Next, you will be presented with a screen asking you to confirm whether you want to install the “Core” and “Main” branches of RetroPie.
Select “Yes” to this option to begin the RetroPie installation process. Please note that this process can take some time as your Raspberry Pi we need to download and install numerous packages.
 
8. Once the installation process has completed, you will be taken back to the main menu of the Retropie setup script.
The next step of setting up our Raspberry Pi with RetroPie is to allow it to autostart the emulation station software. Lucky for us this is a relatively simple process as the Retropie setup script handles it.
To proceed with enabling autostart, go into the “Configuration / Tools” menu.
 
9. Within the “Configuration / Tools” menu you will need to find and select the “autostart” option
 
10. Within this menu, you will want to select the first option labeled “Start Emulation Station at boot“.
This option will make the EmulationStation frontend for RetroPie boot up when the Raspberry Pi powers on. This option saves you from needing to start the software manually.
 
11. Once selected, we can now restart our Raspberry Pi to make sure everything is working as it should be.
Start by pressing “ESC” until you get back to the main menu.
Once on the main menu, select the “Perform reboot” option to reboot the Raspberry Pi.
 
Upon rebooting the Raspberry Pi should end up showing the EmulationStation startup screen. This screen indicates that you have successfully setup the RetroPie software on your Raspberry Pi.
Adding ROMS for the Raspberry Pi RetroPie Emulators
ROM is short for read-only memory and is the format in which you will find pretty much all the classic games.
 
ROMs can be easily found on the internet and since there many different sources it’s best just to google the game you wish to download followed by ROM, e.g. (“Doom ROM”).
There are three different primary methods for transferring ROMS over to your RetroPie, this being USB, SFTP, and SAMBA. We will explore all three different methods below.
Copying ROMs from a USB Drive
1. Before we get started, we need to make sure that the USB service is enabled on RetroPie. If it’s not, then this guide will fail to work as it relies on it to scan and create folders on our USB drive.
Let’s get started by going to the configuration screen within RetroPie. Within this screen, select the “RETROPIE SETUP” option to get into the RetroPie setup tool.
2. We should first ensure that we are running the latest version of the RetroPie setup script by selecting the “Update RetroPie-Setup script“.
3. Within the RetroPie setup tool, go to the “Manage Packages” submenu.
Within here, you will need to go into the “Manage optional packages” menu.
In this menu, search for the “usbromservice” and select it.
Finally, select the “Install from binary” option to install the USB rom service to your Raspberry Pi.
4. With the “usbromservice” now installed and the menu still up, go ahead and select the “Configuration / Options” menu.
Within this menu, select the “Enable USB ROM Service scripts“. This option will setup all the scripts that will monitor the USB devices plugged into the Raspberry Pi.
5. Once done, head back to the main menu of the RetroPie setup tool and select the “Perform Restart” option.
6. With everything set up on the Raspberry Pi, we need to ensure now that the USB drive that you want to use is formatted to the FAT32 format.
You can check this on Windows by right-clicking on the drive, clicking “Properties” and looking at the text next to “File System:“.
 
7. On the USB, create a directory called “retropie“.
The RetroPie USB Rom service software will detect this folder when the USB is plugged in and will prepare the directory for copying over ROMS by creating several folders within it.
 
8. Now plug the USB into the Raspberry Pi, give this a few minutes as the Raspberry Pi RetroPie software will be setting it up in preparation for copying over ROMS.
If your USB has a flashing light, wait until it has stopped flashing before you pull it out.
If it doesn’t have a light, then wait a few minutes for the job to complete.
9. Now take out the USB from the Raspberry Pi and plug it back into the computer.
10. Add the ROMS to their respective folders on the USB.
These folders will be in the retropie/roms folder. (Eg. retropie/roms/snes)
Below we have included a screenshot of what the folder layout should look like after the RetroPie software has created all the needed folders.
 
11. Once you have finished copying your ROMs to the USB, plug it back into the Raspberry Pi.
The RetroPie software will immediately start copying these files off of the USB drive. Don’t take out your USB for some time as this process can take considerable time.
12. Refresh EmulationStation by pressing F4, or choosing “quit” from the start menu.
Copying ROMS over SFTP
1. Before you can utilize SFTP to transfer files between your computer and the Raspberry Pi, you will need first to enable SSH.
You can do this by going to the RetroPie “Configuration” menu within the Emulation Station UI. Within this menu, select “RASPI-CONFIG“.
2. Within the Raspberry configuration tool go to “5 Interfacing Options“, then within that menu select “P2 SSH“.
When asked if you would like to enable the SSH server, select “<Yes>“.
You can now select “<Finish>” on the main menu to return to the RetroPie interface.
3. For copying files over SFTP, you will need to utilize a program such as WinSCP to connect to the Raspberry Pi if you are running Mac use something like Cyberduck.
On Windows, go to WinSCP’s download page and download the latest version of WinSCP.
WinSCP is the tool that will interact with the Raspberry Pi and allow us to copy files directly to the Raspberry Pi.
For those who are running a Mac OS X device, you can find the Cyberduck software within the Mac App Store or by downloading it from Cyberducks website.
For this guide, we will be just be focusing on utilizing the WinSCP software, but the connection details will all remain the same.
4. Once downloaded, launch the WinSCP software. It will immediately ask you for new login details.
You will need to enter the following details into the correct fields.
File Protocol: SFTP
IP address: To find the IP address of your RetroPie, go into RetroPie options from the main menu, and select the last option “Show IP address“.
Port Number: 22 (default)
Username: pi (default)
Password: raspberry (default)
 
5. Once successfully connected to your Raspberry Pi Retropie, you should pay attention to the right-hand side screen.
Locate the folder named “RetroPie“, double-click on that, once within that folder locate the folder named “Roms” and double-click again to enter that folder.
You should now be sitting in the directory where all your roms will be stored.
The file directory displayed at the top should be something like /home/pi/RetroPie/roms.
 
6. Once in the correct folder, all you need to do is drop the files into the appropriate folder for your console.
For example, for a SNES game, you would drag and drop the file onto the folder named “snes“.
The WinSCP software will immediately begin to copy the files you dropped over into the folder. This process can take some time depending on both your hard drive and network speeds.
7. Back on your Raspberry Pi, you can refresh the Emulation Station software by pressing F4, or choosing “quit” from the start menu and relaunching the software.
Your new roms may not show up without refreshing the EmulationStation software.
Copying ROMs over Samba Network shares
A clean installation of RetroPie from their precompiled images has “Samba” pre-installed and enabled by default.
However, if you installed this on Raspbian separately and not from the RetroPie image, you will need to enable it manually.
Samba is the interface that allows Linux and Mac-based devices to connect with Microsoft’s shared network devices interface.
The Samba interface allows you to access the files on your Raspberry Pi over the network without needing to connect with something like WinSCP.
1. If you are running a clean install from the RetroPie image, then you can skip to step 6 of this tutorial.
Otherwise, if you have installed RetroPie to a pre-existing Raspbian installation, you will need to go through a few extra steps to set up this.
To get to the RetroPie setup tool, go to the “Configuration” menu, and select the “RETROPIE SETUP” option.
2. Once the setup script is loaded on your Raspberry Pi, you will be greeted by numerous different options.
Within this menu, find and select the “Configuration / tools” option by using the ARROW keys.
Once you have found the correct option and have it selected, you can press “ENTER” to load it.
 
3. Within this menu, you need to search for the option labeled “samba“.
Once you have selected the “samba” option, press ENTER to prepare the Raspberry Pi for use with SAMBA.
 
4. Selecting this option will install all the packages required to set up and run Samba on your Raspberry Pi.
Once the Raspberry Pi has completed installing all the required packages, you will be met with another screen.
On this screen, you will need to select the “Install RetroPie Samba shares” option.
This option will automatically set up Samba on your Raspberry Pi to share the RetroPie related folders and allow network access to them.
 
5. Once the Samba installation process has completed, you can now safely quit out of the RetroPie software.
There are two ways you can do this, one is to press the CTRL + C combo, and the other is to press ESC and select the “exit” option.
6. Now, back on your computer.
On Windows, open a file explorer window, and in the address bar type in the following.
Note: Make sure you swap out the IP address with your own Raspberry Pi’s IP address.
\\192.168.1.106Copy
 
7. There is a chance it will ask for your login details for your Raspberry Pi.
Just enter your password and username. If you are still using the default user, that will be the following.
Username: pi
Password: raspberry
8. Once in, you can now copy any file you want to your Raspberry Pi.
For copying roms, you will want to go into “roms” and copy the file into the folder of the console it belongs with.
For instance, a SNES game will go in the folder called snes.
Connecting a Network Share to Load ROMs
1. Before you connect up a network share, you must first make sure you have your ROMs are sorted into the structure that the RetroPie software expects.
You can find this folder structure on your Raspberry Pi by using SSH and running the following command.
ls ~/RetroPie/romsCopy
Once you have your ROMs sorted into folders of the same name, we can proceed with connecting the file share with the RetroPie installation.
2. The next thing we need to do is ensure that the Raspberry Pi is set to wait on the network before booting. This wait will ensure that the operating system can perform network connections when it starts up.
To do this, launch up the Raspberry Pi configuration tool by running the command below.
sudo raspi-configCopy
3. Within this menu go to “3 Boot Options“, then select “B2 Wait for Network at Boot“.
When prompted if you would like the boot to wait until a network connection is established, select “<Yes>“.
You can now safely back out of the Raspberry configuration tool.
4. Now with network boot enabled and your drive setup we can proceed to modify RetroPie’s autostart script so that it will automatically mount the drive upon booting.
To do this, we can start modifying the autostart script by running the command below.
sudo nano /opt/retropie/configs/all/autostart.shCopy
5. To the top of this file, add the following line.
You will need to replace several bits of information in this line. We will explain each important bit.
<username> – This text is the username for a user that has access to your shared folder.
<password> – This text is the password to the user you specified.
//REMOTEHOST/roms – This is the network path to where you keep your roms, an example of a valid path is something like “//192.168.0.175/e/ROMs“
sudo mount -t cifs -o username="<username>",password="<password>",nounix,noserverino //REMOTEHOST/roms /home/pi/RetroPie/romsCopy
Once done, go ahead and save the file by pressing CTRL + X followed by Y and then ENTER.
6. Now that we have added the mounting line to the autostart file, we need to go ahead and restart the Raspberry Pi so that it will load in the data from stored on the shared drive.
We can restart the Raspberry Pi by running the command below.
sudo rebootCopy
I hope by the end of this Raspberry Pi RetroPie tutorial you are able to load and play the classics you want. If you want to leave some feedback, then please don’t hesitate to leave a comment below.


