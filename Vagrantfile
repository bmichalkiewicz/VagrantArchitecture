#required to read .yml file
require "yaml"
require "fileutils"

#Load yaml file
architecture = YAML.load_file('hosts.yml')
#create file "inventory"
file = File.open('inventory','w')
architecture.each do |architecture|
  file.puts architecture["group"]
  file.puts architecture["name"] + " ansible_ssh_host=" + architecture["ip"] + " ansible_ssh_user=vagrant" + " ansible_ssh_private_key_file=" + architecture["private_key"]
end
file.close

Vagrant.configure("2") do |config|
#We don't want to insert vagrant private key into vms
config.ssh.insert_key = false

if Vagrant.has_plugin?(vagrant-vbguest)
  config.vbguest.auto_update = false
end

  architecture.each do |architecture|
    config.vm.define architecture["name"] do |server|
      server.vm.box = "bento/centos-7.2"
      server.vm.hostname = architecture["name"]
      server.vm.network "private_network", ip: architecture["ip"]
      server.vm.provider "virtualbox" do |vb|
        vb.name = architecture["name"]  
        vb.cpus = 1
        vb.memory = architecture["memory"]
      end
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "nginx.yml"
    ansible.limit = "all"
    ansible.groups = {
      "haproxy" => ["hp"],
      "webnodes" => ["web1", "web2","web3"],
      "dbs" => ["db1"],
      "all_groups:children" => ["haproxy", "webnodes"]
      }
  end
end