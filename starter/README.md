# Chef Introduction

## Installation Using Vagrant & Virtualbox

### Windows

#### Pre-Steps

* Install Git from https://git-scm.com/download/win
* Install sshwindows from https://sourceforge.net/projects/sshwindows/
* Check git & ssh version on Powershell
* Install Virtualbox from either of
  * https://chocolatey.org/packages/virtualbox/
  * https://www.virtualbox.org/wiki/Downloads
* Install Vagrant from either of
  * https://chocolatey.org/packages/vagrant/
  * https://www.vagrantup.com/downloads.html

#### Setup PATH Verification

Verify git installation in Powershell 
```
PS > git --version
```

Verify ssh installation in Powershell
```
PS > ssh
```

Verify VBoxManage 

To check if VBoxManage is available in system path, simply run the 
```
VBoxManage --version 
```
command. If not found setup the PATH as follows
```
PS > $path = [Environment]::GetEnvironmentVariable("PATH", "Machine")
PS > $vbox_path = "C:\Program Files\Oracle\VirtualBox"
PS > [Environment]::SetEnvironmentVariable("PATH", "$path;$vbox_path", "Machine")
```

Verify Vagrant

To check if VBoxManage is available in system path, simply run the 
```
VBoxManage --version 
```
command. If not found setup the PATH using following command
```
PS > $path = [Environment]::GetEnvironmentVariable("PATH", "Machine")
PS > $vagrant_path = "C:\HashiCorp\Vagrant\bin"
PS > [Environment]::SetEnvironmentVariable("PATH", "$path;$vagrant_path", "Machine")
```

### Other Platforms

TODO

### Setting up using Virtualbox

Add Ubuntu virtual box using Vagrant 

```
vagrant box add bento/ubuntu-14.04 --provider=virtualbox
```

Initalise an Ubuntu Virutalbox
```
mkdir starter
cd starter
vagrant init bento/ubuntu-14.04
```

this palces a default Vagrantfile into the directory. Edit the Vagrantfile like so

```ruby

	config.vm.define "chef-starter" do |chef|
		chef.vm.box = "bento/ubuntu-14.04"
		chef.vm.provider :virtualbox do |vbox|
      vbox.name = "chef-starter"
    end		
  end

```

save the file and start the VM

```
vagrant up
```

you should see similar output
```
MacBook-Pro-2:starter anadi$ vagrant up
Bringing machine 'chef-starter' up with 'virtualbox' provider...
==> chef-starter: Importing base box 'bento/ubuntu-14.04'...
==> chef-starter: Matching MAC address for NAT networking...
==> chef-starter: Checking if box 'bento/ubuntu-14.04' is up to date...
==> chef-starter: Setting the name of the VM: chef-starter
==> chef-starter: Clearing any previously set network interfaces...
==> chef-starter: Preparing network interfaces based on configuration...
    chef-starter: Adapter 1: nat
==> chef-starter: Forwarding ports...
    chef-starter: 22 (guest) => 2222 (host) (adapter 1)
==> chef-starter: Booting VM...
==> chef-starter: Waiting for machine to boot. This may take a few minutes...
    chef-starter: SSH address: 127.0.0.1:2222
    chef-starter: SSH username: vagrant
    chef-starter: SSH auth method: private key
    chef-starter: Warning: Remote connection disconnect. Retrying...
    chef-starter:
    chef-starter: Vagrant insecure key detected. Vagrant will automatically replace
    chef-starter: this with a newly generated keypair for better security.
    chef-starter:
    chef-starter: Inserting generated public key within guest...
    chef-starter: Removing insecure key from the guest if it's present...
    chef-starter: Key inserted! Disconnecting and reconnecting using new SSH key...
==> chef-starter: Machine booted and ready!
==> chef-starter: Checking for guest additions in VM...
==> chef-starter: Mounting shared folders...
    chef-starter: /vagrant => /Users/anadi/Code/meetup/chef-devops/starter
```

Once started login to the VM 

```
vagrant ssh
```

You should see an ubuntu prompt if everything goes fine

```
MacBook-Pro-2:starter anadi$ vagrant ssh
Welcome to Ubuntu 14.04.5 LTS (GNU/Linux 3.13.0-103-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

 System information disabled due to load higher than 1.0

vagrant@vagrant:~$
```

Update system and install curl 

```
vagrant@vagrant:~$ sudo apt-get update
vagrant@vagrant:~$ sudo apt-get -y install curl
```

Install Chef development Kit

```
curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable -v 1.2.22-1
```

> 1.2.22-1 is the latest stable version of Chef at the time of writing this guide (26/Feb/2017), check Chef website for latest version

That's it we are ready to roll!
