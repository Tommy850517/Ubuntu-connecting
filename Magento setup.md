# **Magento website安裝步驟**

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
  - Edit default file
    - ![image](https://github.com/Tommy850517/Ubuntu-connecting/blob/bab49b8252510c5ad79be7c35e9e47deb6f78b28/default.PNG)

* Mariadb
  - https://mariadb.org/download/
    - systemctl status mariadb
    - mariadb --version
  - [Setting](https://www.mageplaza.com/devdocs/how-install-magento-2-ubuntu.html#step-14-update-phpini-file) 
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
 
* [PHP](https://www.mgt-commerce.com/tutorial/how-to-install-magento-2-4-4-on-ubuntu-20-04/)
  - By default PHP 8.1 is not available in Ubuntu 20.04. Use the command below to add a repository for it.
    - sudo apt install software-properties-common && sudo add-apt-repository ppa:ondrej/php -y
    - sudo apt update
    - sudo apt install php8.1-{bcmath,common,curl,fpm,gd,intl,mbstring,mysql,soap,xml,xsl,zip,cli}
  - GOTO /etc/php/8.1/fpm/php.ini and set (sudo nano)
    - memory_limit = 768M
    - upload_max_filesize = 128M
    - zlib.output_compression = on
    - max_execution_time = 18000

* Elastic Search
  - Elasticsearch is not available in the Ubuntu 20.04 repository. 
  - We have to add the Elasticsearch repository to the system. (From https://www.elastic.co/guide/en/elastic-stack-get-started/7.16/get-started-elastic-stack.html)
    - curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.16.3-amd64.deb
    - sudo dpkg -i elasticsearch-7.16.3-amd64.deb
    - sudo /etc/init.d/elasticsearch start
    - sudo systemctl --now enable elasticsearch
  - Run the following command to verify that Elasticsearch is working
    - curl -X GET "localhost:9200"
      ![image](https://github.com/Tommy850517/Ubuntu-connecting/blob/2e438a59cb094223ee4c8758e431fa304ffd13ad/elastic%20search%20success.PNG)
      
* Composer
  - Install
    - curl -sS https://getcomposer.org/installer -o composer-setup.php
    - sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
  - Check version
    - composer -v
* Magento install
  - [Marketplace](https://account.magento.com/applications/customer/login/?client_id=10906dd964b2dcc6befafab4f567ce6b&redirect_uri=https%3A%2F%2Fmarketplace.magento.com%2Fsso%2Faccount%2FoauthCallback%2F&response_type=code&state=e39f7055574e055fd238caec5d1b1afd)
    - Create an account and new access key

  - composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.4.4 /opt/magento2
    
  - php bin/magento setup:install \
    --base-url=http://example.com \
    --db-host=localhost \
    --db-name=magento2 \
    --db-user=tommy \
    --db-password=Tommy850517123 \
    --admin-firstname=admin \
    --admin-lastname=admin123 \
    --admin-email=admin@admin.com \
    --admin-user=admin \
    --admin-password=admin \
    --language=en_US \
    --currency=USD \
    --timezone=America/Chicago \
    --use-rewrites=1
  - Correct the permissions
    - sudo chown -R www-data. /opt/magento2
  - Disable two-factor authentication
    - sudo -u www-data bin/magento module:disable Magento_TwoFactorAuth
    - sudo -u www-data bin/magento cache:flush 
  
* reference: https://www.mgt-commerce.com/tutorial/how-to-install-magento-2-4-4-on-ubuntu-20-04/
