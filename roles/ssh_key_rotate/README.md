SSH_Key_Rotate
=========

SSH_key_Rotate is a role for changing ssh private keys on all servers specified in the running playbook.  The role 
also publishes each device's public key to all other device's authorized_keys.  

Requirements
------------

Currently, the inventory file will need to use hostnames instead of IP Addresses or DNS aliases.  This can be changed
if needed by changing the "Fetch the keyfile from the remote device to the Ansible server" task (second to last)

Role Variables
--------------

Defaut variables are maintained in: ssh_key_rotate/vars/main.yml 
These variables can be overridden by passing them in your playbook as shown in the Example Playbook section below:

username: user_to_change
key_name: id_rsa  
host_group: test_group         

Note: "host_group" variable can be the same inventory group as hosts: defined in your playbook or it can be different.
If "hosts:" and "host_group:" are the same, the net result is every device in your group will all over devices public 
keys added to the authorized_keys file.  If "hosts:" and "host_group" are different, the net result is every device in
"hosts" will have their public keys added to the authorized_keys file on each of the devices in "host_group".  

Dependencies
------------

Requires gather_facts: yes

Example Playbook
----------------

If you need to "restore" key based authentication with your servers you can use the ansible-playbook -k option to 
pass your SSH Password in to your playbook.     
 
      hosts: servers
      gather_facts: yes
      roles:
         - { role: ssh_key_rotate, username: 'override_user', key_name: 'override_id_rsa', host_group: 'override_group' }


License
-------

                    GNU GENERAL PUBLIC LICENSE
                       Version 3, 29 June 2007

Author Information
------------------

GitHub Repository: https://github.com/robertholl/Ansible_Roles
