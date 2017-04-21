Vagrant.require_version '>= 1.7.0'

Vagrant.configure(2) do |config|
  config.vm.box = 'ubuntu/trusty64'

  # config.ssh.insert_key = false

  config.vm.provider 'virtualbox' do |v|
    v.name = 'arrr_demo'
    v.linked_clone = true
    v.memory = 1024
    v.cpus = 2
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.sudo = true
    ansible.playbook = 'playbook.yml'
  end
end
