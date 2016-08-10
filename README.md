# Integration-of-DevStack-with-ldap

System requirements :  Devstack attempts to support Ubuntu 14.04/16.04, Fedora 23/24, CentOS/RHEL 7, as well as Debian and OpenSUSE.
 If you do not have a preference, Ubuntu 16.04 is the most tested, and will probably go the smoothest.

Steps to integrate devstack with ldap

1) Cloning Devstack liberty
git clone https://github.com/openstack-dev/devstack.git -b stable/liberty
If git is not installed install it by sudo apt-get install git

2) Go into devstack
cd devstack

3) Download the localrc file and paste it into the devstack folder

4) Execute the following command
./stack.sh
This will take a 15 - 20 minutes, largely depending on the speed of your internet connection. Many git  packages will be installed during this process. At the end of this in the terminal you will get success message like this

Horizon is now available at http://10.0.2.15/
Keystone is serving at http://10.0.2.15:5000/v2.0/
Examples on using novaclient command line is in exercise.sh
The default users are: admin and demo
The password: password
ldap password : password
This is your host ip: 10.0.2.15
stack.sh completed in 269 seconds.


5) Install PHPldapadmin
sudo apt-get install phpldapadmin

6) Configure PHPldapadmin
sudo gedit /etc/phpldapadmin/config.php

7) Search for the following sections and modify them accordingly.
Replace dc=test,dc=com with dc=openstack,dc=org
$servers->setValue('server','base',array('dc=test,dc=com'));

Replace cn=admin,dc=test,dc=com with cn=Manager,dc=openstack, dc=org
$servers->setValue('login','bind_id','cn=admin,dc=test,dc=com');

Make the following true and uncomment
$config->custom->appearance['hide_template_warning'] = true ;

8) Execute the following command and modify the file
sudo gedit /usr/share/phpldapadmin/lib/TemplateRender.php

9) Thats all you are now set go ahead log in to ldap and create user and now you can log in with the same user id in horizon and same applies to horizon .
