# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.hostname = "wordpress"

  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network :private_network, ip: "33.33.33.10"

  config.ssh.forward_agent = true

  config.berkshelf.enabled = true
  config.omnibus.chef_version = :latest

  config.vm.provision :chef_solo do |chef|
    chef.json = {
      build_essential: {
        compiletime: true
      },
      mysql: {
        server_root_password: 'vagrant',
        server_debian_password: 'vagrant',
        server_repl_password: 'vagrant'
      },
      wordpress: {
        active_plugins: [
          'hello'
        ]
      }
    }

    chef.run_list = [
        "recipe[build-essential]",
        "recipe[application_wordpress::vagrant]"
    ]
  end
end
