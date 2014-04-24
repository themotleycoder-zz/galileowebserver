galileowebserver
================

The following explains how to configure your Galileo to run a nodejs web server

Inital Preperation
------------------
* Format SD Card
* Download the SD Card image from the intel site http://downloadmirror.intel.com/23171/eng/LINUX_IMAGE_FOR_SD_Intel_Galileo_v0.7.5.7z
* Expand the image
* Copy all the files to the SD Card

resize partition
----------------
In a linux distro (I used an ubuntu 14.04 VM on a windows 8 machine)
        
        fsck.ext3 -f /media/yourpath/image-full-clanton.ext3
        resize2fs /media/yourpath/image-full-clanton.ext3 4009600

update node version
-------------------
https://communities.intel.com/servlet/JiveServlet/download/221298-75632/nodejs_0.10.25-r0_i586.ipk.zip

        scp nodejs_0.10.25-r0_i586.ipk root@<ipaddress>:~/
        opkg install ~/nodejs_0.10.25-r0_i586.ipk

node -v
v0.10.25

Fix time issue
--------------
* if you get the following erro trying to run NPM installs: npm ERR! Error: CERT_NOT_YET_VALID
* Run the following command using a valid time server (time servers:http://tf.nist.gov/tf-cgi/servers.cgi)
        
        rdate -s nist-time-server.eoni.com

Install Tools
-------------
        
        npm install -g grunt-cli
        npm install -g bower

Setup Webserver
---------------

