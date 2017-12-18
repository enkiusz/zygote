# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "debian/jessie64"
  config.vm.network "private_network", ip: "192.168.10.2"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant-ssh.yml"
    ansible.groups = {
      "all" => [ 'default' ]
    }
  end

  config.vm.provision "ansible" do |ansible|

    ansible.playbook = "zygotes.yml"
    ansible.groups = {
      "zygotes" => [ 'default' ]
    }
    ansible.host_vars = {
      "default" => {
        "zygote_network" => '{"interface": "eth1","gateway":"192.168.10.1","dns_domain":"provnet0.local"}'
      }
    }
  end
end

