# Cheatsheet on how to setup Windows subsystem for Linux (WSL) for the local development

Linux, Node.js, npm, Git, Apache, PHP, PostgreSQL


## Install subsystem

* press win key
* type Turn Windows Features on or of
* tick Windows Subsystem for Linux
* go to MS store and install your flavor of linux


## Install and setup Node.js and npm

* sudo apt install curl 
* url -sL https://deb.nodesource.com/setup_11.x | sudo bash -
* sudo apt install nodejs

replace setup_11.x with current version</li>


## Update Node.js and npm to the latest version

* sudo npm cache clean -f
* sudo npm install -g n
* sudo n latest

sudo n stable for the stabel version


## Install and setup Git

* sudo apt install git
* git config --global user.email "you@example.com"
* git config --global user.name "Your Name"


## Install and set up Apache, PHP

* sudo apt install apache2
* sudo apt install php


## Install PostgreSQL

### latest for Debian

* sudo apt install wget ca-certificates
* wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
* sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

### latest for Ubuntu

* sudo apt install wget ca-certificates
* wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
* sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ \`lsb_release -cs\`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

### run this for either

* sudo apt-get update
* sudo apt install postgresql postgresql-contrib


### Restart Apache and PostgreSQL

* sudo service apache2 restart
* sudo service postgresql restart


### Set postgres password (to connect from pgAdmin etc)

* sudo su postgres (enter your pass)
* psql
* \password
* \q


### Create a symlink between Windows projects folder and folder on Linux subsystem e.g.

* sudo ln -s /mnt/c/projects /var/www/devroot


### Setup vhost e.g.
```
<VirtualHost *:80>
        ServerName www.test.local
        ServerAdmin mac@localhost
        DocumentRoot /var/www/devroot/projects/test

        <Directory /var/www/>
          Options Indexes FollowSymLinks
          AllowOverride All
          Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/testerror.log
        CustomLog ${APACHE_LOG_DIR}/testaccess.log combined
</VirtualHost>
```


### Edit hosts file on Windows

* press win key
* type in Notepad
* right click and open as Administrator
* with the Notepad open the C:\Windows\System32\Drivers\etc\hosts (make sure all files are selected in the file type dropdown)
* add a new line 127.0.0.1 www.test.local


## Disable terminal's bell sound on tab-completion

* sudo nano /etc/inputrc
* uncomment set bell-style none


## Uning default terminal colours in tmux

* nano ~/.tmux.conf
* paste in
```
set -g default-terminal "xterm-256color"
set-option -ga terminal-overrides ",xterm-256color:Tc"
```
