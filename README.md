Galileo Web Server
==================

The following explains how to configure your Galileo to run a nodejs web server

Inital Preperation
------------------
* Upgrade Galileo firmware to latest version
* Format SD Card
* Download the SD Card image from the intel site http://downloadmirror.intel.com/23171/eng/LINUX_IMAGE_FOR_SD_Intel_Galileo_v0.7.5.7z
* Expand the image
* Copy all the files to the SD Card

Resize Partition
----------------
By default the Intel provided partition is small, you will need to expand it in order to accomodate all the node tools and the web server:
In a linux distro (I used an ubuntu 14.04 VM on a windows 8 machine)
        
        fsck.ext3 -f /media/yourpath/image-full-clanton.ext3
        resize2fs /media/yourpath/image-full-clanton.ext3 4009600
        
Test Connection
---------------
At this point you should be able to SSH to the board

        ssh root@<ip address>
        
If you get an error that says something along the lines of:
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

you will need to use the following command to clean the issue up (replace the number in the parens - in this case 8 - with line number given in the error message)

        perl -pi -e 's/\Q$_// if ($. == 8);' ~/.ssh/known_hosts

You should now be able to SSH to the Galileo and run some basic commands in the environment

Update Node Version
-------------------
The version of node in the image is old and will need to be updated:
https://communities.intel.com/servlet/JiveServlet/download/221298-75632/nodejs_0.10.25-r0_i586.ipk.zip
        
        scp nodejs_0.10.25-r0_i586.ipk root@<ipaddress>:~/
        opkg install ~/nodejs_0.10.25-r0_i586.ipk

Now run the following command and it should come back with a result that establishes that it is v0.10.xx
        node -v
        v0.10.25

Fix time issue
--------------
* if you get the following error trying to run NPM installs: npm ERR! Error: CERT_NOT_YET_VALID
* Run the following command using a valid time server (time servers:http://tf.nist.gov/tf-cgi/servers.cgi)
        
        rdate -s nist-time-server.eoni.com

Install Tools
-------------
        
        npm install -g grunt-cli
        npm install -g bower

Setup Webserver
---------------

