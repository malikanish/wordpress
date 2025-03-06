# Install and Configure WordPress on Ubunt

# Update package lists to get the latest versions
sudo apt update

# Upgrade installed packages to their latest versions
sudo apt upgrade -y

# Install Apache web server
sudo apt install apache2

# Install MySQL database server
sudo apt install mysql-server

# Secure MySQL installation (set root password, remove test DB, etc.)
sudo mysql_secure_installation

# Install PHP and required extensions for WordPress
sudo apt install php libapache2-mod-php php-mysql php-curl php-xml php-mbstring php-zip

# Navigate to the /tmp directory
cd /tmp

# Download the latest WordPress package
wget https://wordpress.org/latest.tar.gz

# Extract WordPress archive
tar xzvf latest.tar.gz

# Move WordPress files to the web server root directory
sudo mv wordpress/* /var/www/html/

# Set correct ownership for WordPress files
sudo chown -R www-data:www-data /var/www/html/

# Set appropriate permissions for WordPress files
sudo chmod -R 755 /var/www/html/

# Login to MySQL as root
sudo mysql -u root -p

# Create a database for WordPress
CREATE DATABASE wordpress;

# Create a new MySQL user for WordPress
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'password';

# Grant all privileges to the WordPress user
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';

# Apply privilege changes
FLUSH PRIVILEGES;

# Exit MySQL
EXIT;

# Navigate to WordPress directory
cd /var/www/html

# Copy the sample configuration file
sudo cp wp-config-sample.php wp-config.php

# Edit WordPress configuration file
sudo nano wp-config.php

# Update database credentials inside wp-config.php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wpuser');
define('DB_PASSWORD', 'password');

# Access WordPress installation page in a web browser
# Go to http://your_vm_ip_address

