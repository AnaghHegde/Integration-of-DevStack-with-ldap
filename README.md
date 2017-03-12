# Integration-of-DevStack-with-ldap </br>

System requirements :  Devstack attempts to support Ubuntu 14.04/16.04, Fedora 23/24, CentOS/RHEL 7, as well as Debian and OpenSUSE.
 If you do not have a preference, Ubuntu 16.04 is the most tested, and will probably go the smoothest.

Steps to integrate devstack with ldap </br>

1) Cloning Devstack liberty </br>
```**Note:** You can use any of this if you want use anything other than liberty you should change it correspondingly in the localrc file also.
```

`git clone https://github.com/openstack-dev/devstack.git -b stable/liberty </br>`

`git clone https://github.com/openstack-dev/devstack.git -b stable/newton </br>`

`git clone https://github.com/openstack-dev/devstack.git -b stable/ocata </br>`

If git is not installed install it by sudo apt-get install git </br>

2) Go into devstack </br>
`cd devstack` </br>

3) Download the localrc file and paste it into the devstack folder </br>

4) Execute the following command </br>
`./stack.sh` </br>
This will take a 15 - 20 minutes, largely depending on the speed of your internet connection. Many git  packages will be installed during this process. At the end of this in the terminal you will get success message like this </br>

Horizon is now available at http://10.0.2.15/ </br>
Keystone is serving at http://10.0.2.15:5000/v2.0/ </br>
Examples on using novaclient command line is in exercise.sh </br>
The default users are: admin and demo </br>
The password: password </br>
ldap password : password </br>
This is your host ip: 10.0.2.15 </br>
stack.sh completed in 269 seconds. </br>


5) Install PHPldapadmin </br>
`sudo apt-get install phpldapadmin`

6) Configure PHPldapadmin </br>
`sudo gedit /etc/phpldapadmin/config.php` </br>

7) Search for the following sections and modify them accordingly. </br>
Replace dc=test,dc=com with dc=openstack,dc=org </br>
$servers->setValue('server','base',array('dc=test,dc=com')); </br>

Replace cn=admin,dc=test,dc=com with cn=Manager,dc=openstack, dc=org </br>
$servers->setValue('login','bind_id','cn=admin,dc=test,dc=com'); </br>

Make the following true and uncomment </br>
$config->custom->appearance['hide_template_warning'] = true ;</br>

8) Execute the following command and modify the file </br>
`sudo gedit /usr/share/phpldapadmin/lib/TemplateRender.php` </br>

9) Thats all you are now set go ahead log in to ldap and create user and now you can log in with the same user id in horizon and same applies to horizon .</br>
