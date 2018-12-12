#required to read .yml file
require "yaml"
require "fileutils"

# IMPORTANT -> CHECK YOUR SSH KEY AND PUT PATH BELOW
sshpath=

#Load yaml file
architecture = YAML.load_file('hosts.yml')
#create file "inventory"
file = File.open('inventory','w')
architecture.each do |architecture|
  file.puts architecture["group"]
  #Please change here path to your private_key. check your key with this command: vagrant ssh-config | grep IdentityFile
  file.puts architecture["name"] + " ansible_host=" + architecture["ip"] + " ansible_user=vagrant" + " ansible_ssh_private_key_file=./.vagrant/machines/" + architecture["name"] + "/virtualbox/private_key"
end
file.close

Vagrant.configure("2") do |config|
#We don't want to insert vagrant private key into vms
#config.ssh.insert_key = false

if Vagrant.has_plugin?("vagrant-vbguest")
  config.vbguest.auto_update = false
end

  architecture.each do |architecture|
    config.vm.define architecture["name"] do |server|
      server.vm.box = "bento/centos-7.2"
      server.vm.hostname = architecture["name"]
      server.vm.network "private_network", ip: architecture["ip"]
      server.vm.provider "virtualbox" do |vb|
        vb.name = architecture["name"]  
        vb.default_nic_type = "82543GC"
        vb.cpus = 1
        vb.memory = architecture["memory"]
      end
    end
  end

  #config.vm.provision "ansible" do |ansible|
    #ansible.playbook = "nginx.yml"
    #ansible.limit = "all"
    #ansible.inventory_path = "inventory"
  #end
end