# check_perm_systemd - Checking permissions on files called by systemd root services
Find scripts / binaries called from systemd services with root privilege that have bad write permissions.


The program goes through every service file in '/ect/systemd/system' checks which scripts are called in
'ExecStart=' or similar blocks. Then it goes through the file permissions of these scripts and looks for
writeable files by non-root users.

This was mainly done to see how some basic file utilities work in python and also to find some files
where I forgot to change the permissions. Basically try to put user services into '~/.config/systemd/user' or change file permissions accordingly.


## Systemd
See the documentation [here](https://www.freedesktop.org/wiki/Software/systemd/).
Systemd is a "System and Service Manager" for Linux operating systems.
You can define a service file in /etc/systemd/service and these services can be called by the 
service daemon if certain conditions are met. Users can define these service files and allow them to run
commands or scripts on the system. However, if not further specified these scripts will run with root permission.
If the script has write permission for the user, all or certain groups this is a security issue.

In case you want to run user services don't forget to specify the user in the service file ('User=' entry) or
you can also put services in '~/.config/systemd/user'.
If the script really needs to be run from a root service, change owner and group of the script to root, change
write permissions to be non-writeable.

## Installing and Usage
1. clone the repo
`git clone git@github.com:Laeri/check_perm_systemd.git`

2. run the python script

`cd check_perm_systemd/`

`./check_perm_systemd`

## License
This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file
for details.
