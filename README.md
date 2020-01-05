# README.md
A demonstration of how to use Vagrant to bring up a default Ubuntu VM on virtualbox.  

## Prequisites
[Vagrant Setup](https://www.vagrantup.com/intro/getting-started/project_setup.html)

### Installation of Vagrant and Ansible
Install on MacOS
```
brew cask install ansible
brew install vagrant
```

Install on Linux
```
apt install ansible
apt install vagrant
```

Creating a default Vagrantfile
```
vagrant init hashicorp/bionic64
```

```
ansible-galaxy role list
ansible-galaxy install nickjj.docker
ansible-galaxy install gantsign.oh-my-zsh 
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


## Troubleshooting

[Issue with Vagrant 2.2.6 and VirtualBox 6.1](https://github.com/oracle/vagrant-boxes/issues/178)

[Bridged Networking](https://github.com/daftlabs/creed/wiki/Set-up-Vagrant-network-bridge)
