# Ansible Deploy N number of Users on Remote servers
This script is designed to use Ansible to deploy n number of users on remote users and distribute their remote ssh PRIVATE and PUBLIC keys to allow for completely passwordless ssh.

**Requirements:**
* Ansible

##How to Deploy Users
1. Open *create_n_users.yml* 
2. Modify list of variables contained inside, particularly:
  *  user:  the base of the username, in this case, testuser
  *  start:  the starting number, in this case 0
  *  end:  the ending number in this case 10
  *  local: This is the directory on the local PC that the ansible script will be running on.
3. ansible-playbook create_n_users.yml

##What it will do
###Master:

1. On the master server where you want the users to be created, n users will be created with their ssh keys and home directory's created. 

2. Creates the authorized users file in the .ssh directory

3. Downloads all of the home directories local to where the script is running.  (This is a potential security issue.)

###Slave:

1. Creates n users on the rest of the machines 

2. Copies all of home directories that were stored local to all of the remote slave locations

###Local host:

1. Deletes all of the downloaded home directories

### Notes:
1. This does transfer public and private keys so for sensitive data be careful. 
2. This script should be used on users who do not exist already
3. As always, with anything dealing with home directories, be careful
4. Similiar to above, I take no responsibility for loss of data.

##How is this playbook licensed?

It's licensed under the Apache License 2.0. The quick summary is:

> A license that allows you much freedom with the software, including an explicit right to a patent. “State changes” means that you have to include a notice in each file you modified. 

[Pull requests](https://github.com/JamesOBenson/Ansible-deploy-n-users/pulls) and [Github issues](https://github.com/JamesOBenson/Ansible-deploy-n-users/issues) are welcome!

-- James