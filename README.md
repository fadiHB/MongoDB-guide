# MongoDB 3.6 for WSL2 | Ubuntu

## Uninstall the MongoDB

1. Stop MongoDB.  
Stop the mongod process by issuing the following command.  
`sudo service mongodb stop`

2. Remove Packages.  
Remove any MongoDB packages that you had previously installed.  
`sudo apt-get purge mongodb-org*`

3. Remove Data Directories.  
Remove MongoDB databases and log files.  
`sudo rm -r /var/log/mongodb`  
`sudo rm -r /var/lib/mongodb`  
or by using one command  
`sudo rm -r /var/log/mongodb /var/lib/mongodb`

* Extra commands to make sure everything is uninstalled.  
`sudo apt-get purge mongodb mongodb-clients mongodb-server mongodb-dev`  
`sudo apt-get purge mongodb-10gen`  
`sudo apt-get autoremove`  

Some of those commands may fail, depending on what packages you actually have installed, but that's okay.

This should also remove your config from /etc/mongodb.conf.

### Note

if you did the steps in the [Microsoft’s directions](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-database#install-mongodb), you may have created a directory named "data".  
remove this directory for now by:
`rm -rf data`

## install MongoDB in WSL

1. Update & upgrade your Ubuntu packages.  
`sudo apt-get update` // Fetches the list of available updates  
`sudo apt-get upgrade` // Strictly upgrades the current packages

2. Install MongoDB packages.  
`sudo apt-get install mongodb`

3. Confirm installation and get the version number.  
`mongo --version`

4. Run the server.  
`sudo service mongodb start`

5. Start mongo console.  
`mongo`

* Check the service status.  
`sudo service mongodb status`

### Start MongoDB using the operating system's built-in init system

In the example above we ran MongoDB directly. Other tutorials may start MongoDB using the operating system's built-in init system. You might see the command `sudo systemctl status mongodb` used in tutorials or articles. Currently WSL does not have support for systemd (a service management system in Linux).

You shouldn't notice a difference, but if a tutorial recommends using sudo systemctl, instead use: `sudo /etc/init.d/`.

* For example:  
`sudo systemctl status mongodb`, for WSL would be `sudo /etc/init.d/mongodb status` ...or you can also use `sudo service mongodb status`.

### Repair

* In some cases, you may have a problem while starting the service.  
Try to do a repair by following these steps:

  1. Remove lock file.  
    `sudo rm /var/lib/mongodb/mongod.lock`

  2. Repair mongodb.  
    `mongod --repair`

  3. Start mongodb.  
    `sudo service mongodb start`

  4. Start mongo console.  
    `mongo`
    
* When you do a repair and see this error " exception in initAndListen: NonExistentPath: Data directory /data/db not found "
in this case, you shoud do the following:
  1. Make a directory to store data:   
  `mkdir -p data/db`
  2. Run a Mongo instance:   
  `sudo mongod --dbpath ~/data/db`
  3. Repair mongodb.  
    `mongod --repair`
  4. Start mongodb:    
  `sudo service mongodb start`

* If you have error " Unit mongodb.service is masked ":    
  * run this: `sudo systemctl unmask mongodb` or `sudo /etc/init.d/mongodb unmask`

If that did not works, you probably faced a problem during the installation.  
try to uninstall and install again.
