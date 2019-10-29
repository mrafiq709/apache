# Apache-Install-Ubuntu
Apache Server Configuration Ubuntu

Note: Before set up Apache you must have to install PHP: https://github.com/mrafiq709/PHP-install-ubuntu

Command:
---------
    sudo apt update
    sudo apt install apache2
    sudo ufw app list
    sudo ufw allow 'Apache'
    sudo ufw status
    sudo systemctl status apache2
    sudo systemctl restart apache2
    http://your_server_ip
    
Give Permission To Access Your Project:
---------------------------------------
    sudo mkdir /var/www/html/my_project
    sudo chown -R $USER:$USER /var/www/html/my_project
    sudo chmod -R 755 /var/www/html/my_project
    
If you have no project then create index.html for testing:
----------------------------------------------------------
    nano /var/www/html/my_project/index.html
    Enter bellow code for testing:
    "<html>
    <head>
        <title>Welcome to Your_domain!</title>
    </head>
    <body>
        <h1>Success!  The your_domain virtual host is working!</h1>
    </body>
    </html>"
    
Setting Up Virtual Hosts:
--------------------------
    sudo nano /etc/apache2/sites-available/project_name.conf
    
    <VirtualHost *:80>
        ServerAdmin webmaster@example.com
        ServerName example.com
        ServerAlias www.example.com
        DocumentRoot /var/www/html/my_project_name/public
           <Directory /var/www/html/my_project_name/public>
                Options -Indexes
                DirectoryIndex index.php index.html
                AllowOverride All
                Require all granted
          </Directory>
        ErrorLog ${APACHE_LOG_DIR}/my_project_name-error.log
        CustomLog ${APACHE_LOG_DIR}/my_project_name-access.log combined
    </VirtualHost>
    
Second Virtual Host [if you want to add another project]:
---------------------------------------------------------

    <VirtualHost *:80>
        ServerAdmin webmaster@example.com
        ServerName test.com
        ServerAlias www.test.com
        DocumentRoot /var/www/html/my_second_project_name/public
          <Directory /var/www/html/my_second_project_name/public>
                Options -Indexes
                DirectoryIndex index.php index.html
                AllowOverride All
                Require all granted
          </Directory>
        ErrorLog ${APACHE_LOG_DIR}/my_second_project_name-error.log
        CustomLog ${APACHE_LOG_DIR}/my_second_project_name-access.log combined
    </VirtualHost>
    
Enable the New Virtual Host Files:
-----------------------------------
    sudo a2ensite example.com.conf
    sudo a2ensite test.com.conf
    
disable the default site defined in 000-default.conf:
-------------------------------------------------------
    sudo a2dissite 000-default.conf
    
 Now restart Apache server:
 ---------------------------
    sudo service apache2 restart
    
If you haven’t been using actual domain names that you own to test this procedure and have been using some example domains instead, you can at least test the functionality of this process by temporarily modifying the hosts file on your local computer.

    sudo nano /etc/hosts
    
The details that you need to add are the public IP address of your VPS server followed by the domain you want to use to reach that VPS.

For the domains that I used in this guide, assuming that my VPS IP address is 111.111.111.111, I could add the following lines to the bottom of my hosts file:

    127.0.0.1   localhost
    127.0.1.1   guest-desktop
    111.111.111.111 example.com
    111.111.111.111 test.com
    
Test your Results:
-------------------
    http://example.com
    http://test.com

References
------------
https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-16-04
