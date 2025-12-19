# PHP-FPM + Apache + MySQL Setup

Install and configure PHP-FPM with Apache and MySQL on Debian for local development.

> ⚠️ **Warning**
>  
> It is highly recommended that you do **NOT** use these instructions on a production server.

---

## 📑 Index

- [PHP-FPM + Apache + MySQL Setup](#php-fpm--apache--mysql-setup)
  - [Server Requirements](#server-requirements)
    - [PHP Extensions](#php-extensions)
    - [Install All PHP Requirements](#install-all-php-requirements)
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

### PHP Extensions

**Ctype** – enabled by default  

**cURL**
```bash
sudo apt install php-curl
```

**DOM** – enabled by default  

**Fileinfo** – enabled by default  

**Filter** – enabled by default  

**Hash** – enabled by default  

**Mbstring**
```bash
sudo apt install php-mbstring
```

**OpenSSL** – enabled by default  

**PCRE** – enabled by default  

**PDO (MySQL)**
```bash
sudo apt install php-mysql
```

**Session** – enabled by default  

**Tokenizer** – enabled by default  

**XML**
```bash
sudo apt install php-xml
```

**BCMath (optional)**
```bash
sudo apt install php-bcmath
```

**FastCGI Process Manager (FPM)**
```bash
sudo apt install php-fpm
```

**Zip**
```bash
sudo apt install php-zip
```

---

### Install All PHP Requirements

```bash
sudo apt install php php-fpm php-mbstring php-xml php-mysql php-curl php-zip php-bcmath -y
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
ALTER USER 'root'@'localhost'
IDENTIFIED WITH mysql_native_password
BY 'secret';
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
