<h1 align="center">
LaraCommerce REST API
</h1>

<h5 align="center">
REST API for E-Commerce platform with admin panel integration.
</h5>

<p align="center">
    <a href="https://github.com/muhammadhabibfery/laracommerce-api/actions/workflows/ci.yml">
    <img alt="GitHub Workflow Status" src="https://img.shields.io/github/actions/workflow/status/muhammadhabibfery/laracommerce-api/ci.yml?logo=github">
    <a href="https://www.php.net">
        <img src="https://img.shields.io/badge/php-%3E%3D8.1-%23777BB4" />
    </a>
    <a href="https://laravel.com">
        <img src="https://img.shields.io/badge/laravel-9.x-%23EC4E3D" />
    </a>
</p>

</br>

| [Admin Panel Features][] | [Requirements][] | [Install][] | [How to setting][] | [API Docs][] | [License][] |

## Admin Panel Features 
- <img src="public/images/admin-panel.png" alt="Preview" width="75%"/>

- |<h3>Menu  </h3>        |       Description                                                                 |
  |-----------------------|-----------------------------------------------------------------------------------|
  |<b>Users               | </b>Create employee and manage all users.                                         |
  |<b>Orders              | </b>Manage the orders.                                                            |
  |<b>Finances            | </b>Manage the finances.                                                          |
  |<b>Withdraw            | </b>Manage the merchant's withdraw request.                                       |
  |<b>Bankings            | </b>Create and manage available banking for merchant.                             |
  |<b>Categories          | </b>Create and manage available category for merchant's products.                 |
  |<b>Profile             | </b>Edit user's profile and password.                                             |


## Requirements

	PHP = ^8.1.x
    laravel = ^9.x
    kavist/rajaongkir = ^1.x
    midtrans/midtrans-php = ^2.x
    laravel/scout = ^9.x
    filament/filament = ^2.x
    beyondcode/laravel-websockets = ^1.x
    pusher/pusher-php-server = ^7.x
    flowframe/laravel-trend = ^0.1.x
    barryvdh/laravel-debugbar = ^3.x
    laravel-echo = ^1.15.x
    pusher-js = ^8.x

## Install

To deploy your Laravel project using Nginx, MySQL, and an SSL certificate on an Ubuntu server, and then upload a README file to your GitHub repository, follow these steps:

### 1. **Set Up Your Server**
- **Update your server:**
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```

- **Install necessary packages:**
  ```bash
  sudo apt install nginx mysql-server php-fpm php-mysql git -y
  ```

- **Secure MySQL:**
  ```bash
  sudo mysql_secure_installation
  ```
  Follow the prompts to set a root password, remove anonymous users, disallow root login remotely, and remove the test database.

### 2. **Set Up MySQL Database**
- **Login to MySQL:**
  ```bash
  sudo mysql -u root -p
  ```
  
- **Create a database and user for your Laravel project:**
  ```sql
  CREATE DATABASE laravel_db;
  CREATE USER 'laravel_user'@'localhost' IDENTIFIED BY 'password';
  GRANT ALL PRIVILEGES ON laravel_db.* TO 'laravel_user'@'localhost';
  FLUSH PRIVILEGES;
  EXIT;
  ```

### 3. **Set Up Laravel**
- **Clone your Laravel project:**
  ```bash
  cd /var/www/html
  sudo git clone https://github.com/yourusername/your-laravel-project.git
  cd your-laravel-project
  ```

- **Install Composer dependencies:**
  ```bash
  sudo apt install composer -y
  composer install
  ```

- **Set up environment file:**
  ```bash
  cp .env.example .env
  nano .env
  ```
  Update the `.env` file with your database and other configuration details:
  ```env
  DB_DATABASE=laravel_db
  DB_USERNAME=laravel_user
  DB_PASSWORD=password
  ```

- **Generate an application key:**
  ```bash
  php artisan key:generate
  ```

### 4. **Set Up Nginx**
- **Create a new Nginx configuration file:**
  ```bash
  sudo nano /etc/nginx/sites-available/laravel
  ```

- **Add the following configuration:**
  ```nginx
  server {
      listen 80;
      server_name your_domain_or_IP;
      root /var/www/html/your-laravel-project/public;

      index index.php index.html index.htm index.nginx-debian.html;

      location / {
          try_files $uri $uri/ /index.php?$query_string;
      }

      location ~ \.php$ {
          include snippets/fastcgi-php.conf;
          fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
          fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
          include fastcgi_params;
      }

      location ~ /\.ht {
          deny all;
      }
  }
  ```

- **Enable the configuration and restart Nginx:**
  ```bash
  sudo ln -s /etc/nginx/sites-available/laravel /etc/nginx/sites-enabled/
  sudo nginx -t
  sudo systemctl restart nginx
  ```

### 5. **Set Up SSL with Certbot**
- **Install Certbot and the Nginx plugin:**
  ```bash
  sudo apt install certbot python3-certbot-nginx -y
  ```

- **Obtain and install the SSL certificate:**
  ```bash
  sudo certbot --nginx -d your_domain_or_IP
  ```

- **Follow the prompts to configure the SSL certificate.**

### 6. **Set Up Permissions**
- **Give Nginx ownership of the Laravel directory:**
  ```bash
  sudo chown -R www-data:www-data /var/www/html/your-laravel-project
  sudo chmod -R 755 /var/www/html/your-laravel-project
  ```

### 7. **Finalize the Laravel Setup**
- **Run migrations:**
  ```bash
  php artisan migrate
  ```

- **Optimize Laravel:**
  ```bash
  php artisan optimize
  ```






[Download Node.js](https://nodejs.org/en/download/)


NPM dependencies
```
npm install
```

Run Vite

```
npm run dev
```

## How to setting 

Go into .env file change Database and Email credentials. Then setup some configuration with your own credentials
```
PUSHER_APP_ID=justRandomString
PUSHER_APP_KEY=justRandomString
PUSHER_APP_SECRET=justRandomString
PUSHER_HOST=127.0.0.1
PUSHER_PORT=6001
PUSHER_SCHEME=https|http   (Just choose one)
PUSHER_APP_CLUSTER=mt1

RAJAONGKIR_API_KEY=<Your-API-Key>

MIDTRANS_SERVER_KEY = <Your-Server-Key>
MIDTRANS_PRODUCTION = false
MIDTRANS_SANITIZED = true
MIDTRANS_3DS = true|false   (Just choose one)

<!-- If you are using algolia, change the scout_driver and setting your own algolia credentials -->
SCOUT_DRIVER=database

<!-- If you are using laravel valet and https protocol, add your valet path below -->
LARAVEL_WEBSOCKETS_SSL_LOCAL_CERT='/Users/YOUR-USERNAME/.config/valet/Certificates/VALET-SITE.TLD.crt'
LARAVEL_WEBSOCKETS_SSL_LOCAL_PK='/Users/YOUR-USERNAME/.config/valet/Certificates/VALET-SITE.TLD.key'
LARAVEL_WEBSOCKETS_SSL_PASSPHRASE=''

```

Run the migration

```
php artisan migrate
```

Or run the migration with seeder if you want seeding the related data

```
php artisan migrate --seed
```

Generate a New Application Key

```
php artisan key:generate
```

Create a symbolic link

```
php artisan storage:link
```

## API Docs
<img src="public/images/LaraCommerce-API.png" alt="Preview" width="75%"/>
</br>
<p style="font-weight: bold;">
Complete REST API Documentation can be found <a href="https://documenter.getpostman.com/view/25234064/2s93JnUSRS">here</a>
</p>


## License

> Copyright (C) 2023 Muhammad Habib Fery.  
**[⬆ back to top](#laracommerce-rest-api)**

[Admin Panel Features]:#admin-panel-features
[Requirements]:#requirements
[Install]:#install
[How to setting]:#how-to-setting
[API Docs]:#api-docs
[License]:#license
