# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.hostname = "wordpress"

  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network :private_network, ip: "33.33.33.12"

  config.ssh.forward_agent = true

  config.berkshelf.enabled = true
  config.omnibus.chef_version = :latest

  config.vm.provision :chef_solo do |chef|
    chef.log_level = :debug
    chef.json = {
      build_essential: {
        compiletime: true
      },
      mysql: {
        server_root_password: 'vagrant',
        server_debian_password: 'vagrant',
        server_repl_password: 'vagrant'
      },
      php: {
        secure_functions: {
          # removes proc_open from disabled functions (required for wp-cli)
          disable_functions: 'dl,posix_kill,posix_mkfifo,posix_setuid,proc_terminate,shell_exec,system,leak,posix_setpgid,posix_setsid,proc_get_status,proc_nice,show_source,virtual,proc_terminate,inject_code,define_syslog_variables,syslog,posix_uname'
        }
      },
      wordpress: {
        active_plugins: [
         'hello'
        ]
      }
    }

    chef.run_list = [
        "recipe[build-essential]",
        "recipe[mysql::server]",
        "recipe[application_wordpress::vagrant]"
    ]
  end
end
