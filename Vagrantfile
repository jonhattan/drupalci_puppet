# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

require 'yaml'
vconfig = YAML::load_file('Vagrantfile-config.yaml')


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.forward_agent = true
  config.vm.provision "shell", path: "standalone/install"
  config.vm.provision "shell", path: "standalone/apply"

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = "http://10.0.2.2:3128/"
    config.proxy.https    = "http://10.0.2.2:3128/"
    config.proxy.no_proxy = "localhost,127.0.0.1,.example.com"
  end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.no_remote = true
  end

  hostname = "drupalci"
  config.vm.define hostname, primary: true do |host|
    host_config = vconfig['default'].merge(vconfig.fetch(hostname, {}))

    host.vm.box = host_config['box']
    host.vm.hostname = "drupalci"

    host.vm.provider "virtualbox" do |v|
      v.memory = host_config['memory']
      v.cpus = host_config['cpus']
    end
  end
end

