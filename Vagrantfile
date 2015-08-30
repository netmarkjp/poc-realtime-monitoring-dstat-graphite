# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "puppetlabs/centos-6.6-64-nocm"
  # config.vm.box = "puppetlabs/centos-7.0-64-puppet"
  vhosts = [
    {"name" => "mon00", "ip" => "192.168.33.10", "cpu" => 2, "memory" => 1024},
    {"name" => "mon01", "ip" => "192.168.33.11", "cpu" => 2, "memory" => 1024},
    {"name" => "mon02", "ip" => "192.168.33.12", "cpu" => 2, "memory" => 1024},
  ]
  vhosts.each do |vhost|
    config.vm.define vhost["name"] do |sv|
      sv.vm.hostname = vhost["name"]
      sv.vm.network "private_network", ip: vhost["ip"]
      # sv.vm.network "forwarded_port", guest: 80, host: 8080
      # sv.vm.network "private_network", ip: "192.168.33.10"
      # sv.vm.network "public_network"
      # sv.vm.synced_folder "../data", "/vagrant_data"
      sv.vm.provider "virtualbox" do |vb|
        vb.cpus = vhost["cpu"]
        vb.memory = vhost["memory"]
        vb.customize ["modifyvm", :id, "--ioapic", "on"]
      end
    end
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.host_key_checking = false
  end
end
