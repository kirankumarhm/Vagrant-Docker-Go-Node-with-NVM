# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "bento/ubuntu-18.04"
  config.vm.hostname = "ubuntu-host"


  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.50.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
  
  config.vm.provision "shell", inline: <<-SHELL
	sudo echo "Asia/Kolkata" | sudo tee /etc/timezone
	sudo apt install -y build-essential curl git libssl-dev man
	sudo apt install resolvconf
	sudo echo "# Make edits to /etc/resolvconf/resolv.conf.d/head." >> /etc/resolvconf/resolv.conf.d/head
	sudo echo "nameserver 8.8.4.4" >> /etc/resolvconf/resolv.conf.d/head
	sudo echo "nameserver 8.8.8.8" >> /etc/resolvconf/resolv.conf.d/head
	sudo service resolvconf restart
	sudo echo "Installing docker and docker-compose"
    	sudo apt update
    	sudo apt install -y software-properties-common curl apt-transport-https ca-certificates 
    	sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
    	sudo apt-key fingerprint 0EBFCD88
	sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    	sudo apt update
    	sudo apt install -y docker-ce
	sudo docker info
	sudo echo "Adding user to docker group"
    	sudo usermod -aG docker $SUDO_USER
	sudo echo "Installing docker-compose"
	# sudo curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/bin/docker-compose
	sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
	sudo chmod +x /usr/bin/docker-compose
	sudo apt install openjdk-11-jre-headless
	sudo echo "Installing Go Lang"
	sudo wget https://go.dev/dl/go1.17.7.linux-amd64.tar.gz
	sudo tar -C /usr/local -xzf go1.17.7.linux-amd64.tar.gz
	sudo rm -f go1.13.3.linux-amd64.tar.gz
	echo "export GOROOT=/usr/local/go" >> /home/vagrant/.profile
	echo "export GOROOT=/usr/local/go" >> /home/vagrant/.bashrc
	echo "export GOPATH=/vagrant/gocc" >> /home/vagrant/.profile
	echo "export GOPATH=/vagrant/gocc" >> /home/vagrant/.bashrc
	echo "export PATH=$PATH:/usr/local/go/bin" >> /home/vagrant/.profile
	echo "export PATH=$PATH:/usr/local/go/bin" >> /home/vagrant/.bashrc
	echo "export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64" >> /home/vagrant/.profile
	echo "export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64" >> /home/vagrant/.bashrc
	echo "export PATH=$PATH:$JAVA_HOME/bin" >> /home/vagrant/.profile
	echo "export PATH=$PATH:$JAVA_HOME/bin" >> /home/vagrant/.bashrc

  SHELL
  
  config.vm.provision "shell", path: "provision.sh", privileged: false

end
