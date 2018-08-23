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
User@UbuntuMachine $ ./setup.bin
```
To set variables when an update is released:

```
user@UbuntuMachine $ sudo vi setup.bin
```

##BOOT ORDER:
1. System sets user-selected variables
2. System installs latest docker from docker repo
3. System checks for git installs
4. Namespaces are obfusicated
5. NGINX is started without priveledge escalations
	-NGINX is listening for connections to port 80 to proxy them to tor
	-This method of doing this allows further modules to be added to the cluster in the future while using NGINX to be the domain controller
6. Tor is started as a proxy service
	-Using tor this way allows users to connect to the host machine using ssh and use a web browser of their choosing


