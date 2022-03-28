$script_mysql = <<-SCRIPT
	apt-get update && \
	apt-get install -y mysql-server-5.7 && \
	mysql -e "create user 'phpuser'@'%' identified by 'pass';" 
SCRIPT

$script_nginx = <<-SHELL
	apt-get update
	apt-get install -y nginx
SHELL

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/bionic64"
  
  #host-only private network
  config.vm.network "private_network", ip: "192.168.56.5"
  
  #interface as local bridge dhcp - vagrantup.com/docs/networking/public_network
  #config.vm.network "public_network"
  
  # forward port if NAT enabled
  config.vm.network "forwarded_port", guest: 80, host: 8080
  
  config.vm.provision "shell", inline: $script_nginx
  
  config.vm.provision "shell", inline: $script_mysql  
  config.vm.provision "shell", inline: "cat /config/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf"
  config.vm.provision "shell", inline: "service mysql restart"
  
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "./config", "/config"
  
end
