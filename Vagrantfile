# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure('2') do |config|
  config.vm.box      = 'ubuntu/trusty64'
  config.vm.hostname = 'conceptql-dev-box'

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'ansible/01_playbook.yml'
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'ansible/02_playbook.yml'
  end
end
