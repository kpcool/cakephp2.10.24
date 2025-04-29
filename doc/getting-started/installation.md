# Installation

This guide will help you install CakePHP 2.x on your system.

## Requirements

- PHP 5.2.8 or greater
- mbstring PHP extension
- intl PHP extension
- PDO PHP extension
- MySQL 4 or greater (if using MySQL)
- Apache with mod_rewrite enabled (recommended)

## Downloading CakePHP

You can download CakePHP in several ways:

1. **Using Composer** (Recommended):
   ```bash
   composer create-project --prefer-dist cakephp/app:^2.10 my_app_name
   ```

2. **Download from GitHub**:
   - Visit [CakePHP GitHub repository](https://github.com/cakephp/cakephp)
   - Download the latest 2.x release
   - Extract the archive to your web server's document root

3. **Using Git**:
   ```bash
   git clone -b 2.x https://github.com/cakephp/cakephp.git
   ```

## Permissions

CakePHP requires write permissions for the following directories:

- `app/tmp`
- `app/Config`
- `app/webroot`

On Unix/Linux systems, you can set the permissions with:
```bash
chmod -R 755 app/tmp
chmod -R 755 app/Config
chmod -R 755 app/webroot
```

## Setup

1. **Development Setup**:
   - Copy `app/Config/core.php.default` to `app/Config/core.php`
   - Copy `app/Config/database.php.default` to `app/Config/database.php`
   - Configure your database settings in `app/Config/database.php`
   - Set `Security.salt` and `Security.cipherSeed` in `app/Config/core.php`

2. **Production Setup**:
   - Follow the same steps as development setup
   - Set `debug` to 0 in `app/Config/core.php`
   - Ensure proper file permissions
   - Configure your web server

## Web Server Configuration

### Apache Configuration

1. Enable mod_rewrite
2. Create an .htaccess file in your document root with:
   ```apache
   <IfModule mod_rewrite.c>
      RewriteEngine on
      RewriteRule ^$ app/webroot/ [L]
      RewriteRule (.*) app/webroot/$1 [L]
   </IfModule>
   ```

3. Create an .htaccess file in app/webroot with:
   ```apache
   <IfModule mod_rewrite.c>
      RewriteEngine On
      RewriteCond %{REQUEST_FILENAME} !-d
      RewriteCond %{REQUEST_FILENAME} !-f
      RewriteRule ^(.*)$ index.php?url=$1 [QSA,L]
   </IfModule>
   ```

### Nginx Configuration

```nginx
server {
    listen 80;
    server_name myapp.local;
    root /path/to/your/app/webroot;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

## Fire It Up

After completing the installation:

1. Point your browser to your application's URL
2. You should see the CakePHP welcome page
3. If you see any errors, check your:
   - File permissions
   - Database configuration
   - Web server configuration
   - PHP version and extensions

## Troubleshooting

Common issues and solutions:

1. **White Screen of Death**:
   - Check PHP error logs
   - Verify file permissions
   - Ensure all required PHP extensions are installed

2. **Database Connection Issues**:
   - Verify database credentials
   - Check if the database server is running
   - Ensure the database exists

3. **URL Rewriting Issues**:
   - Verify mod_rewrite is enabled
   - Check .htaccess files are in place
   - Ensure your web server configuration allows .htaccess overrides 