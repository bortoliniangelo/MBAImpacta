$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server-5.7 && \
  mysql < /vagrant/mysql/script/user.sql && \
  mysql < /vagrant/mysql/script/schema.sql && \
  mysql < /vagrant/mysql/script/data.sql && \
  cat /vagrant/mysql/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf && \
  service mysql restart
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 1
  end

  config.vm.define "mysqlserver" do |mysqlserver|
    mysqlserver.vm.network "private_network", ip: "192.168.56.10"
    mysqlserver.vm.network "forwarded_port", guest: 3306, host: 3306
    mysqlserver.vm.provider "virtualbox" do |vb|
    mysqlserver.name = "mysqlserver"
	config.vm.synced_folder ".", "/vagrant"
    end

    mysqlserver.vm.provision "shell", inline: $script_mysql
  end

  
end
