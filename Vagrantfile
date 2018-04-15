# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.ssh.insert_key = false
  glusterfs_version = "3.13"
  
  # Allocate Resoure
  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.cpus = 1
  end

  # Manage Host
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true

  # Install Tools  
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum -y install net-tools
    sudo yum -y install telnet 
    sudo yum -y install sshpass
  SHELL
  
  # We setup three nodes to be gluster hosts
  N = 3
  (1..N).each do |i|
    config.vm.define vm_name = "gluster-node#{i}" do |config|
      config.cache.scope = :box
      config.vm.hostname = vm_name
      ip = "192.168.56.#{i+50}"
      config.vm.network :private_network, ip: ip      
           
      # Excute after the last VM is booted.    
      if i == N
        config.vm.provision :ansible do |ansible|
          # Disable default limit to connect to all the machines
          ansible.limit = "all"
          ansible.playbook = "playbook.yml"
          ansible.inventory_path = "inventory"
          ansible.verbose  = true
          ansible.become = true        
        end
      end  
    end 
  end
end
