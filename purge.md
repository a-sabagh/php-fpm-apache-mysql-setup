## 📑 Menu

- [Uninstall PHP and Extensions](#uninstall-php-and-extensions)
- [Uninstall MySQL Server with All Configurations](#uninstall-mysql-server-with-all-configurations)
  - [Remove Configuration Files](#remove-configuration-files)
- [Remove Composer Binary File](#remove-composer-binary-file)
  - [Remove Composer Cache & Config](#remove-composer-cache--config)
- [Completely Remove Apache](#completely-remove-apache)
  - [Remove All Apache Configuration, Sites & Logs](#remove-all-apache-configuration-sites--logs)

## Uninstall php and extensions

```bash
sudo apt install php php-fpm php-mbstring php-xml php-mysql php-curl php-zip php-bcmath -y
```

## Uninstall mysql-server with all configurations

```bash
sudo systemctl stop mysql
sudo apt purge -y mysql-*
```

### Remove configuration files

```bash
sudo rm -rf /etc/mysql
sudo rm -rf /var/lib/mysql
sudo rm -rf /var/log/mysql
sudo rm -rf /var/run/mysqld
```

## Remove Composer binary file

```bash
sudo rm -f /usr/local/bin/composer
```
### Remove Composer cache & config

```bash
rm -rf ~/.composer
rm -rf ~/.cache/composer
rm -rf ~/.config/composer
rm -rf ~/.local/share/composer
```
## Completely Remove Apache

```bash
sudo systemctl stop apache2
sudo systemctl disable apache2
sudo apt purge -y apache2*
sudo apt purge -y libapache2-*
```

### Remove all Apache configuration, sites & logs

```bash
sudo rm -rf /etc/apache2
sudo rm -rf /var/www
sudo rm -rf /var/log/apache2
sudo rm -rf /var/run/apache2
```

## Auto Remove

```bash
sudo apt autoremove -y --purge
sudo apt autoclean -y
```
