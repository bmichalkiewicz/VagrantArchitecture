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

Then just run the command `vagrant up` and your VM should bootstrap itself into existence, ready to work with. 

[More information on working with Vagrant VMs, including how to shell into a running VM and shut it down safely, is available in the Vagrant documentation.](http://docs.vagrantup.com/v2/getting-started/index.html)






