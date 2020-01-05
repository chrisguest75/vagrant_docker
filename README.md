# README.md
A demonstration of how to use Vagrant to bring up a default Ubuntu VM on virtualbox.  

## Prequisites
[Vagrant Setup](https://www.vagrantup.com/intro/getting-started/project_setup.html)

### Installation of Vagrant
Install on MacOS
```
brew cask install ansible
brew install vagrant
```

Install on Linux
```
apt install vagrant
```

Creating a default Vagrantfile
```
vagrant init hashicorp/bionic64
```

## Build the VM

```
vagrant up
vagrant provision
```

## Remove VM
```
vagrant destroy
```

