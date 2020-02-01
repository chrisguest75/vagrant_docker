# README.md
A demonstration of how to use Vagrant to bring up a default Ubuntu VM on virtualbox.  
## TODO
1. Build a template vagrantfile

## Prequisites
[Vagrant Setup](https://www.vagrantup.com/intro/getting-started/project_setup.html)

### Installation of Vagrant and Ansible
Install on MacOS 

Tested on vagrant: 2.2.7 & ansible 2.9.2

```
brew install ansible
brew cask install vagrant
```

Install on Linux
```
apt install ansible
apt install vagrant
```

Install role dependencies
```
ansible-galaxy role list
ansible-galaxy install nickjj.docker
ansible-galaxy install gantsign.oh-my-zsh 
```

Creating a new default Vagrantfile
```
vagrant init hashicorp/bionic64
```

## Build the VM

### Network
```
VBoxManage list bridgedifs | grep ^Name
```

Change Vagrantfile with adapter name
```
config.vm.network "public_network", :bridge => "enp0s25: Ethernet"
```

## 
NOTE: If provision is not working it may be because you have an old version of vagrant 
```
vagrant up
vagrant provision
```

```
vagrant up --provider virtualbox --provision
```

## Reboot VM
```
vagrant reload
```

## Remove VM
```
vagrant destroy
```
## Connect VM 
```
vagrant ssh
```

or

```
ssh -i ./.vagrant/machines/default/virtualbox/private_key -l vagrant -o StrictHostKeyChecking=no -p 2222 127.0.0.1
```

## Troubleshooting

[Issue with Vagrant 2.2.6 and VirtualBox 6.1](https://github.com/oracle/vagrant-boxes/issues/178)

[Bridged Networking](https://github.com/daftlabs/creed/wiki/Set-up-Vagrant-network-bridge)
