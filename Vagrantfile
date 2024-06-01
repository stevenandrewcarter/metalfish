# -*- mode: ruby -*-
# vi: set ft=ruby :
NODE_COUNT = 2
Vagrant.configure("2") do |config| 
  config.vm.box = "ubuntu/mantic64"
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end

  (1..NODE_COUNT).each do |i|
    config.vm.define "node#{i}" do |c|
      c.vm.box = "ubuntu/mantic64"
      c.vm.hostname = "node#{i}"
      c.vm.network :private_network, ip: "10.0.0.#{i + 10}"
      c.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "sushy/site.yml"
      end
      c.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--groups", "/baremetal"]      
        v.gui = false        
        v.memory = "512"
      end
    end
  end

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessible to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true

  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
