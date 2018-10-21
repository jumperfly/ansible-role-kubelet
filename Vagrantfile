# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "jumperfly/centos-7-ansible"
  config.vm.box_version = "1804.02.01"
  config.vm.box_check_update = false
  config.vm.provision "shell", run: "always", inline: "swapoff -a"
  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |v|
    v.memory = 512
    v.cpus = 1
  end

  config.vm.provision "shell", inline: <<-SHELL
    mkdir -p /etc/ansible/roles
    ln -snf /vagrant/ /etc/ansible/roles/jumperfly.kubeblet
    ansible-galaxy install --ignore-errors -r /vagrant/tests/requirements.yml -p /etc/ansible/roles
  SHELL

  config.vm.provision "ansible_local" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "tests/test.yml"
  end
end
