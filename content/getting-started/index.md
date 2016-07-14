---
date: 2016-03-09T00:11:02+01:00
title: Getting started
weight: 10
---

## Installation

### Installing Trada

You could install Trada framework project by composer, replace `your-path` with your project name folder

```sh
composer create-project khanhicetea/trada your-path/
```

## Setup

Next, create a virtualhost in your webserver, its document root is `web` folder path. Then reload webservers to enable the web.

### Apache2 virtualhost example
```
<VirtualHost *:80>
        ServerName trada.dev
        DocumentRoot /vagrant/www/trada-demo/web

        ErrorLog ${APACHE_LOG_DIR}/trada.error.log
        CustomLog ${APACHE_LOG_DIR}/trada.access.log combined

        <Directory /vagrant/www/trada-demo/web>
                Options Indexes FollowSymLinks
                AllowOverride All
                Require all granted
        </Directory>
</VirtualHost>
```

### Nginx site example
```
server {
        listen 80;
        server_name trada.dev;
        root /vagrant/www/trada-demo/web;
        index index.php;
        access_log /var/log/nginx/trada.access_log;
        error_log /var/log/nginx/trada.error_log info;
        client_max_body_size 8m;

        location / {
                try_files $uri /index.php$is_args$args;
        }

        location ~ [^/]\.php(/|$) {
            fastcgi_split_path_info ^(.+?\.php)(/.*)$;
            if (!-f $document_root$fastcgi_script_name) {
                return 404;
            }
            fastcgi_index index.php;
            fastcgi_read_timeout 10m;
            fastcgi_pass unix:/run/php/php7.0-fpm.sock;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include fastcgi_params;
        }
}
```

## Configuration

Before you are able to run your website you should take a few minute to adjust some information in the `.env` (copy from `.env.example` and open the file in an editor)

```bash
APP_VENDOR_NAME=App
APP_KEY="This is secret key"

DEBUG=true
WEB_PROFILTER=true

TIMEZONE="Asia/Ho_Chi_Minh"

DB_DRIVER=mysql
DB_HOST=localhost
DB_DATABASE=trada
DB_USERNAME=root
DB_PASSWORD=passwd
DB_CHARSET=utf8
DB_COLLATION=utf8_unicode_ci
```

## Options

### Application config

- Change the `APP_VENDOR` if you want to replace the main namespace of all application classes. (Not recommended)
- Change the `APP_SECRET` could help your application more secure when encrypt the data.

### Debug mode

In order to debug errors (development environment), you should enable `DEBUG=true` to see detail of errors while develop the web.

### Timezone

- Change the `TIMEZONE` by your main application timezone. List of support timezones is [here](https://secure.php.net/manual/en/timezones.php)

### Database config

- `DB_DRIVER` is main database driver, supports :
    - `sqlite` is SQLite
    - `sqlsrv` is SQL Server
    - `mysql` is MySQL
    - `pgsql` is PostgreSQL
- `DB_HOST` is database hostname
- `DB_DATABASE` is database name
- `DB_USERNAME` is database user
- `DB_PASSWORD` is database user password
- `DB_CHARSET` is database charset
- `DB_COLLATION` is database collation

