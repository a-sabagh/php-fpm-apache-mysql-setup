# PHP-FPM + Apache + MySQL Setup

Install and configure PHP-FPM with Apache and MySQL on Debian for local development.

> ⚠️ **Warning**
>  
> It is highly recommended that you do **NOT** use these instructions on a production server.

---

## 📑 Index

- [PHP-FPM + Apache + MySQL Setup](#php-fpm--apache--mysql-setup)
  - [Server Requirements](#server-requirements)
  - [Download and Install Composer Globally](#download-and-install-composer-globally)
  - [Install Laravel Installer](#install-laravel-installer)
  - [MySQL Database](#mysql-database)
  - [Apache Server Installation](#apache-server-installation)
    - [Disable mod_php](#disable-mod-php)
    - [Enable Required Apache Modules](#enable-required-apache-modules)
    - [Enable PHP-FPM Configuration](#enable-php-fpm-configuration)
    - [Install Laravel Application](#install-laravel-application)
    - [Add Laravel Virtual Host](#add-laravel-virtual-host)
    - [Enable site](#enable-site)
    - [Restart Apache](#restart-apache)

---

## Server Requirements

The Laravel framework has a few system requirements.  
Ensure that your server has the required PHP version and extensions installed.

```bash
sudo apt install php php-fpm php-mbstring php-xml php-mysql php-curl php-zip php-bcmath -y
```
## Download and Install Composer Globally

- Download the installer to the current directory
- Verify the installer SHA-384
- Run the installer
- Remove the installer
- Put the composer.phar into a directory on your PATH

```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'c8b085408188070d5f52bcfe4ecfbee5f727afa458b2573b8eaaf77b3419b0bf2768dc67c86944da1544f06fa544fd47') { echo 'Installer verified'.PHP_EOL; } else { echo 'Installer corrupt'.PHP_EOL; unlink('composer-setup.php'); exit(1); }"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
```
---
## Install Laravel Installer

```bash
composer global require laravel/installer
```
Make sure composer path has been added to your global path

```bash
export PATH="~/.config/composer/vendor/bin:$PATH"
```
---
## MySQL Database

Install MySQL using APT:

```bash
sudo apt install mysql-server
```

Login via socket authentication:

```bash
sudo mysql
```

Set the root password (local development only):

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'secret';
```

Run the secure installation script:

```bash
sudo mysql_secure_installation
```

---

## Apache Server Installation

Install Apache:

```bash
sudo apt install apache2 -y
```
### Install Apache Integeration for PHP

```bash
sudo apt install -y libapache2-mod-fcgid
sudo apt install -y libapache2-mod-php
```

### Disable mod_php

```bash
sudo a2dismod php8.3 # phpx.x based on your distro
```

### Enable Required Apache Modules

```bash
sudo a2enmod proxy_fcgi setenvif
```

### Enable PHP-FPM Configuration

```bash
sudo a2enconf php8.3-fpm # phpx.x based on your distro
```

### Set Propert Owner

```bash
sudo chown -R www-data:www-data /var/www/
```

### Install Laravel Application

```bash
laravel new laravel.site

sudo mv ~/www/laravel.site /var/www/laravel.site
```

### ACLs: proper priviledge for all files and directories

```bash
sudo chown -R www-data:www-data storage bootstrap/cache
sudo find storage bootstrap/cache -type d -exec chmod 775 {} +
sudo find storage bootstrap/cache -type f -exec chmod 664 {} +
sudo setfacl -R -m u:www-data:rwx,u:a-sabagh:rwx storage bootstrap/cache
sudo setfacl -R -d -m u:www-data:rwx,u:a-sabagh:rwx storage bootstrap/cache
sudo setfacl -R -m m::rwx storage bootstrap/cache
sudo setfacl -R -d -m m::rwx storage bootstrap/cache
```

### Add Laravel Virtual Host

Generate sample Laravel virtual host `laravel.site.conf`

```apacheconf
<VirtualHost *:80>
    ServerAdmin info@laravel.site
    ServerName laravel.site
    DocumentRoot /var/www/laravel.site/public

    <Directory /var/www/laravel.site>
        AllowOverride All
        Require all granted
        Options FollowSymLinks
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

### Update Hosts

```bash
127.0.0.1 laravel.site
```

### Enable Site

```bash
sudo a2ensite laravel.site.conf
```
### Active Rewirte Module

Activate the rewrite module to enable Laravel to support clean URLs.
```bash
sudo a2enmod rewrite
```

### Restart Apache

```bash
sudo systemctl restart apache2
```
