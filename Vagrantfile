# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 4
  end

  VAGRANT_PLUGINS = %w[vagrant-timezone vagrant-docker-compose vagrant-vbguest]
  VAGRANT_PLUGINS.each do |plugin|
    unless Vagrant.has_plugin?("#{plugin}")
      system("vagrant plugin install #{plugin}")
      exit system('vagrant', *ARGV)
    end
  end

  if Vagrant.has_plugin?("vagrant-timezone")
    config.timezone.value = 'America/Fortaleza' 
  end

  config.vm.provision :docker
  config.vm.provision :docker_compose

  config.vm.synced_folder "./projects", "/home/vagrant/projects",  :mount_options => ["dmode=777", "fmode=777"]

  config.vm.network "forwarded_port", guest: 80, host: 8080

end
