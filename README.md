# vsftpd-backdoor

This is a backdoored version of vsftpd which has been packaged and configured for the convience of performing an example backdoor into a system.
vsftpd was is an FTP server which was created by Chris Evans and is available at vsftpd.beasts.org, this version is 2.3.4.

This backdoor which was maliciously added to the archive was introduced into the vsftpd-2.3.4 2011 
but has since been removed, thus the reason for this repository. 

The diff used in this repo was taken from http://pastebin.com/AetT9sS5

## Changes
Changes to:
* vsftpd.conf to allow remote user login.
* Make file to work with patch.
* Core code, which now includes patch.

## Installation
The installation details are for ubuntu but should be able to be adapted for most distros.

apt-get install build-essential
apt-get install libpam0g-dev


install -v -d -m 0755 /var/ftp/empty 
install -v -d -m 0755 /home/ftp      
groupadd -g 47 vsftpd                
groupadd -g 45 ftp                   
useradd -c "vsftpd User"  -d /dev/null -g vsftpd -s /bin/false -u 47 vsftpd 
useradd -c anonymous_user -d /home/ftp -g ftp    -s /bin/false -u 45 ftp

make

install -v -m 755 vsftpd        /usr/sbin/vsftpd    
install -v -m 644 vsftpd.8      /usr/share/man/man8 
install -v -m 644 vsftpd.conf.5 /usr/share/man/man5 
install -v -m 644 vsftpd.conf   /etc
