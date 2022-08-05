# Raspberry Pi as an NAS server

To create a Raspberry Pi NAS, you will first need to get the necessary equipment. 
- Of course, the minicomputer itself is the focal point: you can choose between the Raspberry Pi 2 and the newer Raspberry Pi 3, both of which have enough power to run the server.
- One SD card for booting Raspberry pi OS Lite (only in terminal mode).
- One SSD OR HDD for storage to share as NAS 

After getting a necessary equipment you will be need to go through following steps.

## STEP 1

- First insert sd card in card reader and plug into you any laptop to install os in sd card by `Respberry pi imager`.

- Select `Respberry Pi OS (other)`

![Screenshot 2022-08-05 at 8 29 36 PM](https://user-images.githubusercontent.com/98619865/183123701-6372993f-fc7c-4c8d-a63d-9cf538a8f1b1.png)


- Select `Respberry Pi OS Light(32-bit or 64-bit)`

![Screenshot 2022-08-05 at 8 29 51 PM](https://user-images.githubusercontent.com/98619865/183123752-feac394f-291d-4c53-b5b6-e83efb8bdc3a.png)


- And select storage 

![Screenshot 2022-08-05 at 8 33 48 PM](https://user-images.githubusercontent.com/98619865/183123777-05715ffb-9943-46ea-982a-4a8be41b2dc4.png)
 

- Before perform write operation press `CTRL+SHIFT+x` and allow ssh and other configuration like wifi. 

 ![Screenshot 2022-08-05 at 8 36 24 PM](https://user-images.githubusercontent.com/98619865/183123807-60cdda4e-4e08-4335-a089-dce9ed5c5afe.png)
 

- Finally perform write operation and take break.
- After install os take out sd card and insert into your credit size minicomputer(Respberry pi) and power on. 
- You will need to access  the `ip` of Raspberry pi do ssh and perform following steps.

Congratulation! , your pi is  ready and accessing via ssh for further configuration.

**First Thing First you have to update and upgrade os first after installation process.**

     sudo apt update && sudo apt upgrade -y

## STEP 2

 If you have the required hardware for your own NAS server, you can devote yourself to installing and setting up the software required to operate it. There are several ways to do this, and one of the most popular ones is to download the GPLv3-licensed `OpenMediaVault`, which has come to be considered the standard.

 - To download and install OpenMediaVault on command line need to clone repo of it and run script to install it.

     `https://github.com/OpenMediaVault-Plugin-Developers/installScript.git`

**This script take long time so take a break for coffe.**

- After installation process of script you will have acces of `web-based interface` of OpenMediaVault. you can simply type Raspberry pi `IP` on web browser.

   ![Screenshot 2022-08-05 at 8 53 58 PM](https://user-images.githubusercontent.com/98619865/183124004-b3c827c3-fa4a-4478-b16e-908578313690.png)
 


- Type default user(`admin`) and password(`openmediavault`) on login interface and your Dashboard look like .

    ![Screenshot 2022-08-05 at 8 56 25 PM](https://user-images.githubusercontent.com/98619865/183124060-5c722140-c4d0-4e75-9e71-6fdc5b4623b1.png)


- Now that time ensure that your SSD or HHD is attached on Respberry pi. After attaching drive you can manage by `OpenMediaVault interface`.

# STEP 3
Make some configuration on OpenMediaVault so it will work as NAS.

- First go to `Storage->Disks` and here is your all drives that are attached on Raspberry pi including root(os) drive(SD card). and now you need to `wipe` your drive(hdd or ssd) that will erase your all data and filesystem.

![Screenshot 2022-08-05 at 10 21 15 PM](https://user-images.githubusercontent.com/98619865/183124493-0ceecb29-7c15-42f4-8a15-93f04356973c.png)


- Second, create a filesystem and mount on it. Go to `Storage->Filesystem` and create and mount drive.

![Screenshot 2022-08-05 at 10 21 52 PM](https://user-images.githubusercontent.com/98619865/183124525-7a9eb114-aff8-43e9-beee-e368b0819f94.png)
![Screenshot 2022-08-05 at 10 22 04 PM](https://user-images.githubusercontent.com/98619865/183124545-c48c7395-977f-4e16-80e8-7bf94742543c.png)


- After mounting create a ` sharefolder `. Go to `Storage->Shared Folder` and create it.
![Screenshot 2022-08-05 at 10 23 43 PM](https://user-images.githubusercontent.com/98619865/183124970-227141c8-1fb7-43ef-8cbb-9a7412b8cb4c.png)


- Finally, it is important to clarify how users can exchange data with the NAS server. SSH (secure shell) is enabled by default, but can only be used by Linux users (through the terminal) without needing additional software. Windows users need client applications such as PuTTY or WinSCP for data transfer through the network protocol.   
  
   A more convenient solution is therefore the cross-platform SMB (Server Message Block), which you can activate under “Services” -> “SMB/CIFS”. Windows has been supporting the protocol by default for years. and also you can activate under “Services” -> “NFS”. for linux and mac users. enable that option and select shared folder.
   
![Screenshot 2022-08-05 at 10 24 30 PM](https://user-images.githubusercontent.com/98619865/183125016-68171b82-06e9-4d10-8c4a-5f5a1c844822.png) 

- Now you also need to configure user password again . Go to `Users->Users->` select user and edit the password.

![Screenshot 2022-08-05 at 10 26 17 PM](https://user-images.githubusercontent.com/98619865/183125112-32076425-33a4-4687-9224-d6fdafa59da1.png)




### Note:-

- The Server Message Block protocol (SMB protocol) is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network. It can also carry transaction protocols for interprocess communication.
- NFS enables system administrators to share all or a portion of a file system on a networked server to make it accessible to remote computer users. Clients with authorization to access the shared file system can mount NFS shares, also known as shared file systems.


**Congratulation ! Your NAS is configured properlly. you are able to acces over that nework.**


### How can accessible?

#### For Window

- Go to `Controlpannel`-> and turn on `networking media shared` option. 
- Open Network folder and you can see here is a device `raspberrypi` and click on it it will ask `user` and `password`  that you have created on `OpenMediaVault interface`. after enter credentials you can see your shared folder. 

#### For mac

- Enter `COMMAND+K` and enter `smb://<ip of raspberrypi>` and connect it so, you are able to access your share folder.


#### After setting up you can also configure as a plex server so it will become so cool.
# How to Setup a Raspberry Pi Plex Server
Go to -> https://pimylifeup.com/raspberry-pi-plex-server/#:~:text=Plex%20is%20a%20client%2Dserver,connect%20to%20the%20same%20server
