# -*- mode: ruby -*-
# vi: set ft=ruby : 

VAGRANTFILE_API_VERSION = "2" 

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  config.ssh.insert_key = false
  config.ssh.pty = true

  config.vm.define "host" do |machine|
    machine.vm.box = "base6"
    machine.vm.synced_folder '.', '/vagrant'
    machine.vm.box_url = "base6.box"
    machine.vm.network :private_network, ip: "10.0.0.10",
                       :netmask => "255.255.0.0"

    machine.vm.hostname = "host"
    machine.vm.provider :virtualbox do |v|
      v.memory = 512
      v.cpus = 2
    end
  end
  
  (1..3).each do |i|
    config.vm.define "node-#{i}" do |node|
    node.vm.box = "base6"
    node.vm.network :private_network, ip: "10.0.0.10#{i}", :netmask => "255.255.0.0"
    node.vm.hostname = "slave#{i}.tst"
    
      node.vm.provider :virtualbox do |v|
	v.memory = 256
      end      
    end
  end
end