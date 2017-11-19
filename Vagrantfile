# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "debian/jessie64"

  config.vm.provision "ansible" do |ansible|

    ansible.playbook = "zygotes.yml"
    ansible.verbose = true
    ansible.groups = {
      "zygotes" => [ 'default' ]
    }
    ansible.raw_arguments = [ "-vvvv" ]
  end
end
