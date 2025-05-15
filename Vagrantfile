# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Configurations for both App and MySQL server.
  config.vm.box = "fedora/39-cloud-base"
  config.vm.box_version = "39.20231031.1"
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 1
    vb.memory = "1024"
    vb.check_guest_additions = false
  end
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Configurations for App server
  config.vm.define "twp-app-sr-01" do |twp_app_sr_01|
    twp_app_sr_01.vm.hostname = "twp-app-sr-01.compute.internal"
    twp_app_sr_01.vm.network "private_network", ip: "10.1.1.5"
    twp_app_sr_01.vm.provider "virtualbox" do |vb|
      vb.name = "twp-app-sr-01"
    end
    twp_app_sr_01.vm.provision "configure-server", type: "shell", path: "app-sr-conf.sh"
    twp_app_sr_01.vm.provision "copy-code", type: "file", source: "../../services", destination: "/opt/twp"
  end

  # Configurations for MySQL server
  config.vm.define "twp-mysql-sr-01" do |twp_mysql_sr_01|
    twp_mysql_sr_01.vm.hostname = "twp-mysql-sr-01.compute.internal"
    twp_mysql_sr_01.vm.network "private_network", ip: "10.1.2.5"
    twp_mysql_sr_01.vm.provider "virtualbox" do |vb|
      vb.name = "twp-mysql-sr-01"
    end
    twp_mysql_sr_01.vm.provision "configure-server", type: "shell", path: "mysql-sr-conf.sh"
    twp_mysql_sr_01.vm.provision "copy-schema", type: "file", source: "../../db/mysql", destination: "/opt/twp/mysql"
  end

end