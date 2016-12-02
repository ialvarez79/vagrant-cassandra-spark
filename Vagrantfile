# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.host_name = "cassandra-spark"
  config.vm.network :private_network, ip: "192.168.10.11"
  config.vm.network :forwarded_port, guest: 22, host: 1233
  config.vm.network :forwarded_port, guest: 8080, host: 8080
  config.vm.network :forwarded_port, guest: 8888, host: 8888  


  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y python
  SHELL

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
  end

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "3096"]
    vb.cpus = 2
  end
end
