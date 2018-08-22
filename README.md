#LinuxTorDocker U+000A
##TL;DR: U+000A
A docker ecosystem for linux servers to run Tor/nginx
to run auto setup type ./setup
make sure you edit setVariables.bin before first use.

##INTRO U+000A
This is a script to automate the creation of docker containers running Tor and NGINX web servers on a Linux ecosystem. This script should do all the heavy lifting for the install. This script was written to run on Ubuntu 16.04 [Xenial Xerus], though it should run on earlier versions of Ubuntu no problem, these have not been tested.

###FIRST USE: U+000A
On first use the setVariables.bin file should be edited (any text editor should do the job).
Make sure the versions you want to use are available and in date. This script does not contain *any* automatic version controls so the responsibility is on you to check versions are correct.

##USER GUIDE: U+000A
Clone the repo or place the file structure into the desired file location then use the following command:

```
User@UbuntuMachine $ ./setup
```
To set variables when an update is released:

```
user@UbuntuMachine $ sudo vi setVariables.bin
```

