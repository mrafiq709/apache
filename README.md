# Apache-Install-Ubuntu
Apache Server Configuration Ubuntu

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
    
Setting Up Virtual Hosts:
--------------------------
    sudo mkdir /var/www/your_domain
    sudo chown -R $USER:$USER /var/www/your_domain
    sudo chmod -R 755 /var/www/your_domain
    nano /var/www/your_domain/index.html
    
    Enter bellow code for testing:
    "<html>
    <head>
        <title>Welcome to Your_domain!</title>
    </head>
    <body>
        <h1>Success!  The your_domain virtual host is working!</h1>
    </body>
    </html>"
    
    sudo nano /etc/apache2/sites-available/your_domain.conf
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
        ErrorLog /var/log/httpd/my_project_name-error.log
        CustomLog /var/log/httpd/my_project_name-access.log combined
    </VirtualHost>
