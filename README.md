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

### Disable mod_php

```bash
sudo a2dismod php8.3
```

### Enable Required Apache Modules

```bash
sudo a2enmod proxy_fcgi setenvif
```

### Enable PHP-FPM Configuration

```bash
sudo a2enconf php8.3-fpm
```

### Restart Apache

```bash
sudo systemctl restart apache2
```
