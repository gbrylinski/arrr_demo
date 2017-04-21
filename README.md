# What? Why?

That's an example playbook utilizing [arrr shared roles](https://github.com/gbrylinski/arrr) and a Vagrantfile simplifying VM provisioning with help of Vagrant.

Please use it as a guideline how to use and configure your Ansible playbook with `arrr` roles.

# Requirements

To test demo playbook Ansible is required. It is probably possible to do that without it but I have no idea why and it's definitely easier with Ansible.

Next we need a machine to provision, most likely a VM. The easiest way to have one is to use e.g. VirtualBox. To simplify and automate creation of VM we can use Vagrant. So:

- **Ansible** - [installing Ansible](http://docs.ansible.com/ansible/intro_installation.html)
- **Vagrant** - [installing Vagrant](https://www.vagrantup.com/docs/installation/)
- **VirtualBox** - [installing VirtualBox](https://www.virtualbox.org/manual/ch02.html)

# Manual installation

To install roles manually we simply need to clone the `arrr` repository into our roles directory:

```shell
cd roles_dir
git clone git@github.com:gbrylinski/arrr arrr
```

next we have to add cloned directory to `roles_path` in `ansible.cfg` file so it knows how to find the roles:

```ini
#
# ansible.cfg file
#
[defaults]
roles_path = ./arrr
```

# Installation with ansible-galaxy

Some smart people some day realized that manual installation can be cumbersome especially if many roles are going to be installed. They created a tool which we can use to make our life a bit easier and named it `ansible-galaxy`. To install `arrr` roles with `ansible-galaxy` we just need to:

```shell
ansible-galaxy -r requirements.yml install
```

next, similarly to manual installation, we need to point Ansible to directory where our installed roles have been written. To do that we have to modify `roles_path` in `ansible.cfg`:

```ini
#
# ansible.cfg file
#
[defaults]
roles_path = roles_dir:roles_dir/arrr
```

Please notice repeated `roles_dir` entry. It's kind of hack to work around the way Ansible tools work. `ansible-galaxy` uses first entry as a base directory to unpack fetched roles. In our case roles would be unpacked into `roles_dir/arrr` which exactly matches second entry.

# Running playbook with Vagrant

It's the simplest way to check how this roles work. To start everything automagically we just need to execute:

```shell
vagrant up --provision
```

Voila! Now it's recommended to get some coffee and see what's new on YouTube. After some minutes machine should be provisioned and ready to use. To ssh to our vagranted machine:

```shell
vagrant ssh
```

That's it. Machine is ready to explore. 

# Running playbook without Vagrant

It's also very simple. All we need is to execute one liner:

```shell
ansible-playbook -i our_inventory_file playbook.yml
```

As you probably noticed we use here an inventory file which needs to exist prior to command execution. For curious people here you may find more information on [ansible inventories](http://docs.ansible.com/ansible/intro_inventory.html).
