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

**[Ctype PHP Extension]([PHP: Ctype - Manual](https://www.php.net/manual/en/book.ctype.php))** : This extension is enabled by default.
**[cURL PHP Extension]([PHP: cURL - Manual](https://www.php.net/manual/en/book.curl.php))**
```bash
apt install php-curl
```
**[DOM PHP Extension]([PHP: DOM - Manual](https://www.php.net/manual/en/book.dom.php))** : This extension is enabled by default.
**[Fileinfo PHP Extension]([PHP: Fileinfo - Manual](https://www.php.net/manual/en/book.fileinfo.php))** : This extension is enabled by default.
**[Filter PHP Extension]([PHP: Filter - Manual](https://www.php.net/manual/en/book.filter.php))** : This extension is enabled by default.
**[Hash PHP Extension]([PHP: Hash - Manual](https://www.php.net/manual/en/book.hash.php))** : The Hash extension is a core PHP extension, so it is always enabled.
**[Mbstring PHP Extension]([PHP: Installation - Manual](https://www.php.net/manual/en/mbstring.installation.php))** : `mbstring` is a non-default extension. This means it
 is not enabled by default. You must explicitly enable the module with the `configure` option.
```bash
apt install php-mbstring
```
**[OpenSSL PHP Extension]([PHP: OpenSSL - Manual](https://www.php.net/manual/en/book.openssl.php) )** : To use PHP's OpenSSL support you must also compile PHP **--with-openssl**.
**[PCRE PHP Extension]([PHP: PCRE - Manual](https://www.php.net/manual/en/book.pcre.php))** : The PCRE extension is a core PHP extension, so it is always enabled. By default, this extension is compiled using the bundled PCRE library.
**[PDO PHP Extension]([PHP: PDO - Manual](https://www.php.net/manual/en/book.pdo.php))** : enabled by php-mysql
```bash
apt install php-mysql
```
**[Session PHP Extension]([PHP: Session Extensions - Manual](https://www.php.net/manual/en/refs.basic.session.php))** : This extension is enabled by default.
**[Tokenizer PHP Extension]([PHP: Tokenizer - Manual](https://www.php.net/manual/en/book.tokenizer.php))** : This extension is enabled by default.
**[XML PHP Extension]([PHP: XML Parser - Manual](https://www.php.net/manual/en/book.xml.php))** : This extension is enabled by default. if missing you can install it using this command:
```bash
apt install php-xml
```
**[BCMath PHP Extension (optional) ]([PHP: BC Math - Manual](https://www.php.net/manual/en/book.bc.php))** : For arbitrary precision mathematics PHP offers BCMath which supports numbers of any size and precision up to `2147483647`decimal digits, if there is sufficient memory, represented as strings.
```bash
apt install php-bcmath
```
**[FastCGI Process Manager (FPM)]([PHP: FastCGI Process Manager (FPM) - Manual](https://www.php.net/manual/en/install.fpm.php))** :
```bash
apt install php-fpm
```
**[Zip PHP Extension]([PHP: Zip - Manual](https://www.php.net/manual/en/book.zip.php))** :
```bash
apt install php-zip
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
