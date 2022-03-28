Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  
  #config.vm.network "private_network", ip: "192.168.59.2"
  
  config.vm.network "public_network"
  
  # forward port if NAT enabled
  config.vm.network "forwarded_port", guest: 80, host: 8080
  
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get install -y nginx
  SHELL
  
end