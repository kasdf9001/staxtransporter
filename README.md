Install Pilvia Stax Vagrant box for development environment
============

Download and install VirtualBox + Vagrant
------------
https://www.vagrantup.com

Linux and Mac OS X hosts has nfs support, more info: https://www.vagrantup.com/docs/synced-folders/nfs.html

On Windows, install WinNFSd plugin for Vagrant. https://github.com/winnfsd/vagrant-winnfsd

vagrant plugin install vagrant-winnfsd

Clone stax and run vagrant box provision
-------------
```shell
git clone https://github.com/pilvia/stax.git
cd stax
mkdir site
vagrant up magento
OR
vagrant up wordpress
```
Go to http://localhost:8080/

Config your setting at ansible/group_vars/all.yml

If you encounter error installing mariadb, try removing ansible/magento.retry file and run:
```shell
vagrant halt magento
vagrant up magento --provision
Go to http://localhost:8080
```

Issues / notes:

* MariaDB install error on Windows (retry works)
* Magerun role installs Magento and it's very slow (atleast on Windows). You can disable this by commenting role magento (and the rest of the lines from magento.yml
* Magerun install is incomplete, partial file content found in core php-scripts --> comment out magento installation from Ansible-scripts
* Using vagrant box as a Magento project submodule?
* To speed up Magento, don't use Vagrant shared folder for running Magento. Instead use rsync or other similar method: Host source code -> Vagrant shared folder -> (rsync) -> Vagrant local Magento install folder




