# Using Ansible
## Vagrant and Ansible
- Using the Vagrantfile here it boots up 3 instances, 1 for the app, 1 for the database and 1 controller vm
- Run `vagrant up` to start the three VMs
- Use `vagrant ssh vm-name` to get into each of them an run `sudo apt-get update -y` this check they are working correctly and connected to the internet
- Return to the controller vm to configure it to use ansible
- Run these commands:
```
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get upgrade -y
sudo apt-get install ansible -y
sudo apt-get install tree
```
- next check you can ssh from the controller to the other two VMs with `ssh vagrant@192.168.33.10` and `ssh vagrant@192.168.33.11`
- if you choose different ips then make sure to change them
- now `cd /etc/ansible` to get to the ansible configuration directory
- use `tree` to see the file structure and file called `hosts` should be present
- this file needs to be configured to allows the controller to run commands in the app and db VMs
- `sudo nano hosts` to edit it
- for the app write this in
```
[web]
192.168.33.10 ansible_connection=ssh ansible_ssh_user=vagrant ansible_ssh_pass=vagrant
```
- for the db write this in
```
[db]
192.168.33.11 ansible_connection=ssh ansible_ssh_user=vagrant ansible_ssh_pass=vagrant
```
- check this has worked by running `ansible all -m ping`
- should get two responses back with pong
### Some extra commands to run
- `ansible all -a "sudo apt-get upgrade -y"` will upgrade all the machines set up in the host file 
