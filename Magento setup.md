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
    - 
