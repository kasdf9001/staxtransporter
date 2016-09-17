Fork of pilvia stax designed for easy transport of files from staging to local vagrant
======================================================================================

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