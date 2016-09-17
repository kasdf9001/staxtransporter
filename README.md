Fork of pilvia stax designed for easy transport of files from staging to local vagrant
======================================================================================

Functionality
=============
Data migration functionality for vagrant machines. The goal is easier initialization
of local environment. Added benefit is that this can be run later on in demand to update
local environment.

* Initializes git in /srv/development/
    * If already initialized, skip (or pull?, clean?)
* Database migration
    * Fetches database information from <path>/app/etc/local.xml or equivalent
    * Dumps database over SSH to vagrant
        * Dump only over SSH, do not litter in remote environment
        * Import the dump in local
        * Overwrite remote url with local url
            * Use wp search-replace with Wordpress
            * Use SQL to replace LIKE %base_url% with Magento
        * Delete SQL dump file
* Use rsync to get rest of files
    * plugins, media uploads etc   

User input requirement
======================

Only the following is required from the user:
* git init url 
* remote username
* remote domain / IP
* remote path
* Magento or Wordpress

examples:
git@github.com:myname/prorepo.git
sofokus
megasite.sofokus.pilvia.io
/srv/staging/
magento

Notes
=====

SSH key from the host needs to be forwarded to the guest, else the staging environment is not accessible. 

<pre>
Please check whether your host system has ssh-agent forwarding enabled. 

You can do so for example by adding this block to your ~/.ssh/config file:
Host                    *
  ForwardAgent          yes 

If this is enabled vagrant ssh (and also vagrant provision) should
 be able to forward your key to the guest machine.

You also might want to check using ssh-add -l whether your ssh-agent 
does know about your SSH-key. If it is in the list and you have 
agent-forwarding activated you should have a success. Otherwise you 
can add the key to your ssh-agent by running ssh-add <path to your key file>.
</pre>
