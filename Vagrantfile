# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2204"
  config.vm.network "private_network", ip: "192.168.56.101"
  config.vm.network "public_network"
  config.vm.synced_folder "MyData", "/vagrant_data"
  config.vm.provider "virtualbox" do |vb|
     vb.memory = "6144"
     vb.cpus = "4"
  end
  config.vm.provision "shell", inline: <<-SHELL
      apt-get update -y
      apt-get install wget curl git vim ca-certificates gnupg lsb-release -y 
      mkdir -p /etc/apt/keyrings
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
      echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      apt-get update -y
      apt-cache policy docker-ce
      apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
      usermod -aG docker vagrant
      sudo systemctl start docker
      sudo enable start docker
      wget https://github.com/docker/compose/releases/download/v2.14.0/docker-compose-linux-x86_64 -O /usr/local/bin/docker-compose
      chmod +x /usr/local/bin/docker-compose
  SHELL
end
