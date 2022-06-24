# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.box = "jeffnoxon/ubuntu-20.04-arm64"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get upgrade -y
     apt-get install -y apt-transport-https ca-certificates curl software-properties-common
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
     add-apt-repository -y "deb [arch=arm64] https://download.docker.com/linux/ubuntu bionic stable"
     apt-get update
     apt-cache policy docker-ce
     apt-get install -y docker-ce
     systemctl enable docker
     systemctl start docker
     systemctl status docker
     apt-get install git
     git clone https://github.com/jecalad/vagrant.git && cd vagrant
     docker build -t devops_vagrant .
     docker run -d -p 80:80 devops_vagrant
  SHELL
end