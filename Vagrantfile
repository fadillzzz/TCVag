# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/trusty64"
    app.vm.synced_folder "../tcp", "/var/www/tcp", type: "rsync", rsync__exclude: ".git/"

    app.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      vb.memory = "1024"
    end

    app.vm.network "forwarded_port", guest: 1337, host: 1337
    app.vm.network "private_network", ip: "192.168.33.11"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "tcp.yml"
    ansible.groups = {
      "app" => ["app"]
    }
    ansible.verbose = "vv"
  end
end