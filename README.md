Vagrant, Ansible and Kubernetes

Prerequisites: On host Machine please install the following tools:

Install Git: https://github.com/git-guides/install-git

Install Virtualbox: https://www.virtualbox.org/wiki/Downloads

Install Vagrant: https://developer.hashicorp.com/vagrant/downloads

Install Ansible: https://docs.ansible.com/ansible/latest/installation_guide/index.html

Usage: Use git to clone this repo and run the commands below:

cd vagrant-ansible-k8

vagrant up

vagrant status

cp .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory InventoryFile

ansible-playbook -i InventoryFile ansible/step01-create-user.yml
