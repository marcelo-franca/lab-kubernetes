# -*- mode: ruby -*-
# vi: set ft=ruby :
required_plugins = %w( vagrant-disksize vagrant-vbguest )
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
  raise "The plugin #{plugin} is required. Please run `vagrant plugin install #{plugin}`"  unless Vagrant.has_plugin? plugin
end

Vagrant.require_version ">= 2.0.0"
VAGRANTFILE_API_VERSION = "2"
TIMEOUT = 600

BOXNAME = "ubuntu/xenial64"
NET_ADDRESS = "192.168.92"
DISKSIZE = "20GB"
DIR_SOURCE = "data/"
DIR_DESTINY = "/vagrant"
DIR_MANIFESTS = "manifests_ansible"
MANIFEST = "k8s.yaml"
ENV["LC_ALL"] = "en_US.UTF-8"
DOMAIN_NAME = "mitlabs.com.br"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = 'auto'
      ansible.playbook = "#{DIR_MANIFESTS}/#{MANIFEST}"
    end


# Prometheus Machine
config.vm.define :prometheus, primary: true do |server_config|
    server_config.vm.provider "virtualbox" do |vb|
        vb.memory = '3072'
        vb.cpus   = '2'
        vb.name   = 'prometheus.mitlabs.com.br'
        vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
    end

    server_config.disksize.size       = DISKSIZE
    server_config.vm.hostname         = 'prometheus.mitlabs.com.br'
    server_config.vm.box              = BOXNAME
    server_config.vm.boot_timeout     = TIMEOUT
    server_config.vm.box_check_update = true
    server_config.vm.network "public_network", ip: "#{NET_ADDRESS}.50", bridge: "enp3s0"
    server_config.vm.synced_folder DIR_SOURCE, DIR_DESTINY   
  end


# Node01 Machine
config.vm.define :alien01, primary: true do |server_config|
    server_config.vm.provider "virtualbox" do |vb|
        vb.memory = '4096'
        vb.cpus   = '2'
        vb.name   = 'alien01.mitlabs.com.br'
        vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
    end

    server_config.disksize.size       = DISKSIZE
    server_config.vm.hostname         = 'alien01.mitlabs.com.br'
    server_config.vm.box              = BOXNAME
    server_config.vm.boot_timeout     = TIMEOUT
    server_config.vm.box_check_update = true
    server_config.vm.network "public_network", ip: "#{NET_ADDRESS}.51", bridge: "enp3s0"
    server_config.vm.synced_folder DIR_SOURCE, DIR_DESTINY   
  end

# Node02 Machine
config.vm.define :alien02, primary: true do |server_config|
    server_config.vm.provider "virtualbox" do |vb|
        vb.memory = '4096'
        vb.cpus   = '2'
        vb.name   = 'alien02.mitlabs.com.br'
        vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
    end

    server_config.disksize.size       = DISKSIZE
    server_config.vm.hostname         = 'alien02.mitlabs.com.br'
    server_config.vm.box              = BOXNAME
    server_config.vm.boot_timeout     = TIMEOUT
    server_config.vm.box_check_update = true
    server_config.vm.network "public_network", ip: "#{NET_ADDRESS}.52", bridge: "enp3s0"
    server_config.vm.synced_folder DIR_SOURCE, DIR_DESTINY   
  end

end
