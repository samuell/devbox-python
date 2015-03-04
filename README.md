# DevBox-Base
*With Docker or Virtualbox as provider and Ansible provisioning*

A Vagrant box (Virtualbox or Docker as providers and Ansible provisioning)
base image, to use as template for setting up specialized development environments.

## Prerequisites

- [Vagrant](https://www.vagrantup.com/)
- [Ansible](http://www.ansible.com/)
- [VirtualBox](https://www.virtualbox.org/) (Not required if you use Docker as provider!)
- [Docker](https://www.docker.com) (Not required if you use Virtualbox as provider!)

### Installing the requirements in Ubuntu (tested with 14.04)

1. Install Virtualbox:
	```bash
	sudo apt-get install virtualbox
	```

2. Install Docker:
	```bash
	sudo apt-get install docker.io
	```

3. Install a recent version of ansible:
   ```bash
   sudo apt-get install ansible/trusty-backports
   ```

   *(if you ubuntu version is "trusty", otherwise, replace it with your appropriate version)*
4. Install Vagrant, by first downloadng the proper .deb file from [vagrantup.com](https://www.vagrantup.com/downloads.html)

5. ... and then installing it with:
	```bash
	sudo dpkg -i <deb-file>
	```

## Setup and Usage

#### Clone the github repository:

```bash
git clone git@github.com:samuell/devbox-base
cd devbox-base
```

#### Bring up the VM

With docker provider (Expect it to take at least ~8m):

```bash
vagrant up docker
```

With VirtualBox provider (Expect it to take at least ~20m):

```bash
vagrant up virtualbox
```

#### Log in to the VM

With docker provider:

```bash
vagrant ssh docker
```

With VirtualBox provider:

```bash
vagrant ssh virtualbox
```

#### A tip on how you can upload your existing git ssh keys to the new vm:

With the following command you can get the info you need to run scp
against the machine:

```bash
vagrant ssh-config [docker | virtualbox]
```

Note the hostname and port number (and identity file, if you with),
and run, for example:

```bash
scp -i <identity-file-path> -P <portno> \
	~/.ssh/id_rsa_<whateveryounamedit> \
	vagrant@<hostname>:/home/vagrant/.ssh/
```

Then, sometimes, in order to get the new key activated in your shell
after logging in to the vm, you might need to do:

```bash
ssh-agent bash -l
ssh-add ~/.ssh/id_rsa_<whateveryounamedit>
```

- Autocompletion will happen automatically
- If you have turned off the YouCompleteMe role, you will get autocompletion with `<C-x><C-o>`

## Known issues

- There are some really red message from the docker daemon when running `vagrant halt`.
  Everything seems to work as expected though (including the shutdown)
- There are some red message on vagrant up, but they are nothing serious, and can be ignored for now.

## References

- [Vagrant & Ansible Quickstart Tutorial](http://adamcod.es/2014/09/23/vagrant-ansible-quickstart-tutorial.html)
