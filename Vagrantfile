# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network "public_network"

    config.vm.hostname = "strut.sc-ict.intranet"

    config.vm.synced_folder "./ansible", "/home/ubuntu/ansible"
    config.vm.synced_folder "./app", "/home/ubuntu/app"

    # install Ansible within the VM and run our dev playbook
    config.vm.provision "ansible_local" do |ansible|
        ansible.install = true
        ansible.provisioning_path = "/home/ubuntu/ansible"
        ansible.playbook = "main.yml"
    end

    # add localhost to Ansible inventory
    config.vm.provision "shell", inline: "printf 'localhost\n' | sudo tee /etc/ansible/hosts > /dev/null"


    config.vm.provider "virtualbox" do |vb|
        # Display the VirtualBox GUI when booting the machine
        # Customize the amount of memory on the VM:
        vb.memory = "2048"
      end

end
