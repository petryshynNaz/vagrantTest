# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Базовий образ
  config.vm.box = "ubuntu/bionic64"

  # Визначення віртуальної машини web
  config.vm.define "web" do |web|
    web.vm.box = "ubuntu/bionic64"
    
    # Хост-онлі мережа
    web.vm.network "private_network", ip: "192.168.56.10"
    
    # Проброс портів
    web.vm.network "forwarded_port", guest: 80, host: 8080

    # Провізія (виправлена)
    web.vm.provision "shell", inline: <<-SHELL
      sudo apt update
      sudo apt install -y nginx
      sudo systemctl enable nginx
      sudo systemctl start nginx
    SHELL
  end

  # Визначення віртуальної машини db
  config.vm.define "db" do |db|
    db.vm.box = "ubuntu/bionic64"
    
    # Хост-онлі мережа
    db.vm.network "private_network", ip: "192.168.56.11"
    
    # Проброс портів
    db.vm.network "forwarded_port", guest: 3306, host: 3309

    # Провізія (виправлена)
    db.vm.provision "shell", inline: <<-SHELL
      sudo apt update
      sudo apt install -y mariadb-server
      sudo systemctl enable mariadb
      sudo systemctl start mariadb
    SHELL
  end
end