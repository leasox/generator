# -*- mode: ruby -*-
# vi: set ft=ruby :

# Specify Vagrant version
Vagrant.require_version ">= 1.6.0"
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    config.vm.synced_folder ".", "/vagrant", disabled: true
    app.vm.provider "docker" do |d|
      d.build_dir = "."
      d.name = "app"
      d.link("db:db")
      d.remains_running = true
      d.volumes = ["/home/ron/Server/test:/app:rw"]
      d.create_args = ["-d", "-P"]
      d.cmd = ["meteor"]
    end
  end

  config.vm.define "db" do |db|
    config.vm.synced_folder ".", "/vagrant", disabled: true
    db.vm.provider "docker" do |d|
      d.image = "tutum/mongodb"
      d.name = "db"
      d.remains_running = true
      d.create_args = ["-d", "-P"]
    end
  end

end