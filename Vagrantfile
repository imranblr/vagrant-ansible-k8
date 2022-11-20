# -*- mode: ruby -*-
# vi: set ft=ruby :

# Specify a custom Vagrant box for the demo
BOX_NAME = "ubuntu/jammy64"


# Vagrantfile API/syntax version.
# NB: Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = BOX_NAME
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = "2"
  end

  config.vm.define "master" do |master|
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.10.14"
    master.vm.provision "file", source: "ansible/k8master", destination: "~/"
    master.vm.provision "shell", inline: "cp -rf /home/vagrant/k8master /home/ubuntu/ && chown ubuntu:ubuntu -R /home/ubuntu"
    master.vm.provision "shell", inline: "apt-get update -qq || true"
    master.vm.provision "shell", inline: "apt-get upgrade -y || true"
    master.vm.provision "file", source: "ansible/hosts", destination: "~/"
    master.vm.provision "shell", inline: "cp -f /home/vagrant/hosts /etc/hosts"
    master.vm.provision "ansible" do |ansible|
      ansible.limit	= "master"
      ansible.verbose	= "True" 
      #ansible.playbook = "ansible/test.yml"
      #ansible.playbook	= "ansible/step01_create_user.yml"
      #ansible.playbook = "ansible/step02_kube-dependencies.yml"
      #ansible.playbook = "ansible/step03_initialize_master.yml"
      #ansible.playbook = "ansible/step04_join_cluster.yml"
      ansible.playbook = "ansible/build-master.yml"

    end
  end

  config.vm.define "worker1" do |worker1|
    worker1.vm.hostname = "worker1"
    worker1.vm.network "private_network", ip: "192.168.10.15"
    worker1.vm.provision "shell", inline: "apt-get update -qq || true"
    worker1.vm.provision "shell", inline: "apt-get upgrade -y || true"
    worker1.vm.provision "file", source: "ansible/hosts", destination: "~/"
    worker1.vm.provision "shell", inline: "cp -f /home/vagrant/hosts /etc/hosts"
    worker1.vm.provision "ansible" do |ansible|
      ansible.limit	= "worker1"
      ansible.verbose	= "True" 
      #ansible.playbook = "ansible/test.yml"
      #ansible.playbook	= "ansible/step01_create_user.yml"
      #ansible.playbook = "ansible/step02_kube-dependencies.yml"
      #ansible.playbook = "ansible/step03_initialize_master.yml"
      #ansible.playbook = "ansible/step04_join_cluster.yml"
      ansible.playbook = "ansible/build-workers.yml"
    end
  end
  
  config.vm.define "worker2" do |worker2|
    worker2.vm.hostname = "worker2"
    worker2.vm.network "private_network", ip: "192.168.10.16"
    worker2.vm.provision "shell", inline: "apt-get update -qq || true"
    worker2.vm.provision "shell", inline: "apt-get upgrade -y || true"
    worker2.vm.provision "file", source: "ansible/hosts", destination: "~/"
    worker2.vm.provision "shell", inline: "cp -f /home/vagrant/hosts /etc/hosts"
    worker2.vm.provision "ansible" do |ansible|
      ansible.limit	= "worker2"
      ansible.verbose	= "True" 
      #ansible.playbook = "ansible/test.yml"
      #ansible.playbook	= "ansible/step01_create_user.yml"
      #ansible.playbook = "ansible/step02_kube-dependencies.yml"
      #ansible.playbook = "ansible/step03_initialize_master.yml"
      #ansible.playbook = "ansible/step04_join_cluster.yml"
      ansible.playbook = "ansible/build-workers.yml"
    end
  end
  
  #config.vm.provision "ansible" do |ansible|

    #ansible.limit          = "all" # or only "nodes" group, etc.
    #ansible.inventory_path = "InventoryFile"
    #ansible.playbook = "ansible/step01_create_user.yml"
    #ansible.playbook = "ansible/install-kubernates.yml"


    #ansible.limit          = "master" # or only "nodes" group, etc.
    #ansible.playbook = "ansible/test.yml" 
    #ansible.playbook = "ansible/update-hosts.yml" 
    #ansible.playbook = "ansible/init-master.yml"

    #ansible.playbook = "ansible/join-k8cluster.yml"
    #ansible.playbook = "ansible/deploy-nginx.yml"
    #ansible.playbook = "ansible/configure-nfs-client.yml"
    #ansible.playbook = "ansible/init-nfs-storageClass.yml"
    #ansible.playbook = "ansible/deploy-runner.yml"
  #end
end

