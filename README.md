# VagrantArchitecture

This bundle of files automates the process of automatically creating and provisioning local virtual machines with a complete, running instance of WordPress, Load Balancer and Database. Such things are useful for local development and testing things like plugins and themes on a "clean" WordPress install.

## Prerequisites

You'll need to have the following prerequisites installed on your workstation, to use these files.

* [VirtualBox](https://www.virtualbox.org/)
* [Vagrant](http://www.vagrantup.com/)
* [Ansible](https://www.ansible.com/)

## What It Does

At file hosts.yml you have configuration of servers (static ip, amount of memory, hostname and so on). Vagrantfile will build virtual machines using this file.

Together with the prerequisites listed above, the scripts contained herein will let you create a new VM with a simple `vagrant up` that:

* Database: MariaDB (database name, login and password can you find as variables in group_vars/all)
* Nginx
* WordPress Version: 4.9.8
* haproxy - Load Balancer

## Getting Started

To begin, create an empty directory and clone the files in this repository into it.

1. The SSH key of your vagrant machine can be displayed with the command: vagrant ssh-config | grep IdentityFile
The output of the command will look like this:

`/home/username/vms/test/.vagrant/machines/default/virtualbox/private_key`

2. Once you got the ssh key path, insert the path to 15 line of the vagrantfile
for example:
file.puts architecture["name"] + " ansible_host=" + architecture["ip"] + " ansible_user=vagrant" + " ansible_ssh_private_key_file=**/path/which/be/displayed/by/command/above**"

3. In the hosts.yml please change ip of the servers. For example 192.168.5.101 etc.

Then just run the command `vagrant up` and your VM should bootstrap itself into existence, ready to work with. 

[More information on working with Vagrant VMs, including how to shell into a running VM and shut it down safely, is available in the Vagrant documentation.](http://docs.vagrantup.com/v2/getting-started/index.html)

## Architecture                                                                                                
 
3 servers with Wordpress, which is assigned to webnodes group in Ansible 
 
- name: web1
  group: "[webnodes]"
  ip: 172.28.128.3

- name: web2
  group: "[webnodes]"
  ip: 172.28.128.4

- name: web3
  group: "[webnodes]"
  ip: 172.28.128.5

LoadBalancer:

- name: hp
  group: "[haproxy]"
  ip: 172.28.128.6

Database for above webnodes.

- name: db1
  group: "[dbs]"
  ip: 172.28.128.7





