#LinuxTorDocker

##TL;DR:
A docker ecosystem for linux servers to run Tor/nginx
to run auto setup type ./setup.bin
make sure you edit setup.bin before first use.

##INTRO 
This is a script to automate the creation of docker containers running Tor and NGINX web servers on a Linux ecosystem. This script should do all the heavy lifting for the install. This script was written to run on Ubuntu 16.04 [Xenial Xerus], though it should run on earlier versions of Ubuntu no problem, these have not been tested.

###FIRST USE:
On first use the setup.bin file should be edited (any text editor should do the job).
Make sure the versions you want to use are available and in date. This script does not contain *any* automatic version controls so the responsibility is on you to check versions are correct.

##USER GUIDE:
Clone the repo or place the file structure into the desired file location then use the following command:

```
User@UbuntuMachine$ ./setup.bin
```
To set variables when an update is released:

```
user@UbuntuMachine$ sudo vi setup.bin
```

##BOOT ORDER:
1. System sets user-selected variables
1. System installs latest docker from docker repo
1. System checks for git installs
1. NGINX is started without priveledge escalations
	1. -NGINX is listening for connections to port 80 to proxy them to tor
	1. -This method of doing this allows further modules to be added to the cluster in the future while using NGINX to be the domain controller
1. Tor is started as a proxy service
	-Using tor this way allows users to connect to the host machine using ssh and use a web browser of their choosing


##MODULARITY

The best part of this build is that the docker ecosystem allows for easy modularity. In order to help *you* with the modularity of this system I will show you the parts of the code that require your editing to work with new containers. I can't help with the containers being added, but I can show you how this system works.

The first requirement is to edit the DN .config file, first navigate to the file located in ```/DN/nginx.conf```.


##To be completed:
Currently the system has many working parts, but few that successfully interact with each other. DTPA (Tor/privoxy container) and DN (Nginx container) work independently, but I have been unable to get them to successfully network with eachother, this is due to issues with Nginx's config file (```DN/nginx.conf```), Privoxys config file (```DTPA/services/privoxy/config```) and Tors torrc file (```DTPA/services/tor/torrc```). These files require a networking configuration I simply have not been able to implement as of yet.

The last two issues with this program as it is, it requires a web browser to install on the host machine so that users accessing it may be able to browse the tor network when connected; it must also install a VNC client on the host machine so that users may connect to it from a windows environment without issue.

###Breakdown of issue:

	* docker-compose.yml must be written into the systemPrepare.bin file so the system can be booted up with the correct configuration every time.

		* Because of this some files require removal (eg:imageBuild.bin). The idea of the docker-compose file is that it should replace all files associated with docker building or running a container.

	* Nginx must be configured as a reverse proxy so it can pass data to the relevant service. In the case of tor it must route all http/https traffic to the waiting privoxy socket [8118].

	* Nginx should have cacheing turned off.

	* Privoxy must be configured to convert http/https traffic into SOCKS5 (see documentation for privoxy)

	* Tor must have the correct configuration, including setting exit node status to 0

	* Browser must be installed

	* VNC must be implemented on the system


##Current Functionality

	* Currently the containers will run in the state they are in, due to the config file issues outlined above the connection is NOT secure at present.
	* The setup.bin file will execute and execute its child scripts
		* setup.bin will prepare the host environment by declaring a number of variables and the running the 'systemPrepare.bin' script, this script is where the majority of the work is done.
		* systemPrepare.bin will then go on to create an unprivelidged user, uninstall old docker versions, get the latest version of docker, repeat this process for git and clone repos. Then the script will try to build an image [this script is now obsolete with the docker-compose.yml file and systemPrepare should be modified to implement this, this includes removing the "docker run" commands.]
