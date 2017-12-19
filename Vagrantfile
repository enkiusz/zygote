# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "debian/jessie64"
  config.vm.define "lynn"

  config.vm.hostname = 'lynn'
  config.vm.provider "virtualbox" do |p|
    p.customize ["modifyvm", :id, "--nic2", "bridged", "--bridgeadapter2", "provnet0"]
  end

  $script = <<SCRIPT
    cat > /etc/network/interfaces.d/provnet0 <<EOF
    iface eth1 inet static
        address 192.168.10.2
        netmask 255.255.255.0
EOF
    ifup eth1
SCRIPT

  config.vm.provision "shell", inline: $script

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant-ssh.yml"
    ansible.groups = {
      "all" => [ 'lynn' ]
    }
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "zygotes.yml"
    ansible.groups = {
      "zygotes" => [ 'lynn' ]
    }
    ansible.host_vars = {
      "lynn" => {
        "zygote_network" => '{"interface": "eth1", "gateway":"192.168.10.1", "dns_domain":"provnet0.local"}'
      }
    }
  end

end

