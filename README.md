# Mongodb

## Uninstall the MongoDB

1. `sudo service mongodb stop`
2. `sudo apt-get purge mongodb-org*`
3. `sudo rm -r /var/log/mongodb`
4. `sudo rm -r /var/lib/mongodb`
5. `sudo apt-get purge mongodb mongodb-clients mongodb-server mongodb-dev`
6. `sudo apt-get purge mongodb-10gen`
7. `sudo apt-get autoremove`

### Note

if you did the steps in the [Microsoft’s directions](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-database#install-mongodb), you may have created a directory named "data", remove this directory by:
`rm -rf data`

## install MongoDB in WSL

1. `sudo apt update`
2. `sudo apt-get install mongodb`
3. `mongo --version`
4. `sudo service mongodb status`
5. `sudo service mongodb start`
6. `sudo /etc/init.d/mongodb status`
7. `mongo`
