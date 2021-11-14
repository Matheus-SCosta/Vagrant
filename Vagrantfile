
# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.network "private_network", ip: "192.168.33.50"
  config.vm.provider "virtualbox" do |vb|
      vb.memory = "2024"
  end
 
  config.vm.provision "shell", inline: <<-SHELL
     
     # Atualizando e instalando o nginx
     sudo apt-get update	
     sudo apt-get install -y nginx

     # Instalando e configurando o mariadb
     sudo apt install mariadb-server -y
     SQL="CREATE DATABASE WordPress CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci; GRANT ALL ON WordPress.* TO WordPressUser @'localhost' IDENTIFIED BY 'your password'; FLUSH PRIVILEGES;"
     mariadb -u root -p -e "$SQL"

     # Baixando o PHP
     sudo apt install -y php7.2-cli php7.2-fpm php7.2-mysql php7.2-json php7.2-opcache php7.2-mbstring php7.2-xml php7.2-gd php7.2-curl
     
     # Baixando e instalando o wordpress
     sudo mkdir -p /var/www/html/sample.com
     cd /tmp
     wget https://wordpress.org/latest.tar.gz
     tar xf latest.tar.gz
     sudo mv /tmp/wordpress/* /var/www/html/sample.com/
     sudo chmod 777 -R /var/www/html/sample.com
     sudo chown -R www-data: /var/www/html/sample.com

     # Clonando repositorio com o arquivo de configuracao do nginx
     git clone https://github.com/Matheus-SCosta/nginx.git
     mv nginx/sampleifpb.com /etc/nginx/sites-available/
 

          

     # Ajuste no nginx
     sudo rm /etc/nginx/sites-available/default
     sudo rm /etc/nginx/sites-enabled/default
     sudo ln -s /etc/nginx/sites-available/sampleifpb.com /etc/nginx/sites-enabled/
     sudo systemctl restart nginx
	
     
	
  SHELL
end
