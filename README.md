# README.md
A demonstration of how to use Vagrant to bring up a default Ubuntu VM on virtualbox.  
## TODO
1. Build a template vagrantfile

## Prequisites
[Vagrant Setup](https://www.vagrantup.com/intro/getting-started/project_setup.html)

### Installation of Vagrant and Ansible
Install on MacOS 

Tested on vagrant: 2.2.7 & ansible 2.9.2

```sh
brew install ansible
brew cask install vagrant
```

Install on Linux
```sh
apt install ansible
apt install vagrant
```

Install role dependencies
```sh
ansible-galaxy role list
ansible-galaxy install nickjj.docker
ansible-galaxy install gantsign.oh-my-zsh 
```

Creating a new default Vagrantfile
```sh
vagrant init hashicorp/bionic64
```

## Build the VM

### Configure Network
```sh
VBoxManage list bridgedifs | grep ^Name
```

Change Vagrantfile with adapter name
```
config.vm.network "public_network", :bridge => "enp0s25: Ethernet"
```

### Build VM
NOTE: If provision is not working it may be because you have an old version of vagrant 
```sh
vagrant up
vagrant provision
```

```sh
vagrant up --provider virtualbox --provision
```

## Reboot VM
```sh
vagrant reload
```

## Remove VM
```sh
vagrant destroy
```
## Connect VM 
Vagrant supports ssh directly to the box
```sh
# if paused
vagrant resume
vagrant ssh
```

But if you would rather use the ssh tool
```sh
ssh -i ./.vagrant/machines/default/virtualbox/private_key -l vagrant -o StrictHostKeyChecking=no -p 2222 127.0.0.1
```

We can also use VSCode to remote-ssh and edit files on the VM
```sh
code --install-extension ms-vscode-remote.remote-ssh
```

```sh
vagrant ssh-config
``` 
then copy the output to ssh-config

```
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /Users/user/Code/scratch/vagrant_docker/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
```

## Upgrading vmadditions

```sh
# Uninstall old version
sudo vbox-uninstall-guest-additions

# Reboot
sudo shutdown -r now

# 1. Open the vm in GUI mode
# 2. Insert the Additions CD 
# 3. /dev/cdrom should exist

sudo mkdir -p /mnt/cdrom
sudo mount /dev/cdrom /mnt/cdrom
sudo sh ./VBoxLinuxAdditions.run --nox11
sudo shutdown -r now

```


## SSH Tunneling
NOTE: Work out how to get this working.
If hosting a service on a port tunnel if to host machine. 
```
ssh -i ./.vagrant/machines/default/virtualbox/private_key -l vagrant -o StrictHostKeyChecking=no -p 2222 -L 8080:127.0.0.1:8080 -N 127.0.0.1 -v
```

## Troubleshooting

[Issue with Vagrant 2.2.6 and VirtualBox 6.1](https://github.com/oracle/vagrant-boxes/issues/178)

[Bridged Networking](https://github.com/daftlabs/creed/wiki/Set-up-Vagrant-network-bridge)

### Time sync
Check timesync if you have issues with certificates
```sh
date
sudo hwclock
sudo VBoxService --timesync-min-adjust 1000
sudo VBoxService --timesync-set-threshold 1000
sudo VBoxService --timesync-interval 60000
```