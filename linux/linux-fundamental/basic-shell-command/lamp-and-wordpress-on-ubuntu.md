# LAMP & WordPress on Ubuntu



```text
#Download Wordpress 
wget http://wordpress.org/latest.tar.gz

#Install Apache, MySQL, and PHP
sudo apt-get install -y apache2 mysql-server php5 php5-gd php5-mysql
#Supply a password for the MySQL root user. Supplying a password will here will
#not change the root password on the Linux server, just the password of the root
#user for the MySQL service.

#Create a MySQL Database
mysql -uroot -p
#Supply the password for the MySQL root account when prompted

#Create a MySQL Database
CREATE DATABASE wordpress;

#Create a MySQL User
CREATE USER wordpress@localhost IDENTIFIED BY 'wppass'; 

#Give the MySQL User Permission to Manipulate the Wordpress Database
GRANT ALL PRIVILEGES ON wordpress.* TO wordpress@localhost;

#Flush the MySQL Privileges
FLUSH PRIVILEGES;

#Exit MySQL
exit 


#Extract the Wordpress Software
cd ~/Dowloads
tar zxvf wordpress-latest.tar.gz

#Configure wordpress
cp wp-config-sample.php wp-config.php
nano wp-config.php
#Replace "database_name_here" with the database created above. (wordpress)
#Replace "username_here" with the MySQL user created above. (wordpress)
#Replace "password_here" with the password for the MySQL user. (wppass)

#Copy the wordpress files into the web server's document root.
cd /var/www
sudo mv html html.bak
sudo mv ~/Downloads/wordpress html
sudo chown -R www-data:www-data html

# Finish the wordpress installation in a web browser.
# firefox http://localhost/
# Give your blog a name.
# Create a user for your blog.
# Supply a password for the user.
# Enter an email address for the user.
# Click "Install Wordpress."

# Log into your Wordpress Installation

```





```

```

