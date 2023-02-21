* Nginx
  - Install
    - sudo apt install nginx
    - sudo ufw app list
    - sudo ufw allow in "Nginx Full"
    - sudo ufw enable
    - sudo ufw status
  
  - Visit http://localhost to check whether success or not
    - sudo systemctl is-active nginx
    - sudo systemctl is-enabled nginx
    - sudo systemctl status nginx

* Mariadb
  - https://mariadb.org/download/
    - systemctl status mariadb
    - mariadb --version
  - [Setting] (https://www.mageplaza.com/devdocs/how-install-magento-2-ubuntu.html#step-14-update-phpini-file) 
    - sudo systemctl restart mariadb.service
    - sudo systemctl enable mariadb.service
    - sudo mysql_secure_installation
  - Create MySQL User
    - sudo mysql -u root -p
    - CREATE DATABASE magento2;
    - CREATE USER 'tommy'@'localhost' IDENTIFIED BY 'Tommy850517123';
    - GRANT ALL ON magento2.* TO 'tommy'@'localhost' IDENTIFIED BY 'Tommy850517123' WITH GRANT OPTION;
    - FLUSH PRIVILEGES;
    - EXIT;
 
* PHP
  - By default PHP 8.1 is not available in Ubuntu 20.04. Use the command below to add a repository for it.
    - sudo apt install software-properties-common && sudo add-apt-repository ppa:ondrej/php -y
    - sudo apt update
    - sudo apt install php8.1-{bcmath,common,curl,fpm,gd,intl,mbstring,mysql,soap,xml,xsl,zip,cli}
    - 
