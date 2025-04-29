# Development Environment

This guide explains how to set up and configure your development environment for CakePHP 2.x.

## Required Software

1. **PHP 5.2.8 or greater**
   - Required extensions:
     - mbstring
     - intl
     - PDO
     - MySQL (if using MySQL)
     - SQLite (if using SQLite)
     - PostgreSQL (if using PostgreSQL)

2. **Web Server**
   - Apache (recommended)
     - mod_rewrite enabled
     - mod_ssl (for HTTPS)
   - Nginx
   - IIS (with URL Rewrite module)

3. **Database**
   - MySQL 4 or greater
   - PostgreSQL
   - SQLite
   - Microsoft SQL Server

4. **Version Control**
   - Git (recommended)
   - SVN
   - Mercurial

## Development Tools

1. **Code Editor/IDE**
   - PHPStorm (recommended)
   - Visual Studio Code
   - Sublime Text
   - NetBeans
   - Eclipse

2. **Debugging Tools**
   - Xdebug
   - DebugKit plugin
   - FirePHP
   - ChromePHP

3. **Database Tools**
   - phpMyAdmin
   - MySQL Workbench
   - pgAdmin
   - SQLite Browser

4. **Version Control Tools**
   - Git
   - GitHub Desktop
   - SourceTree
   - TortoiseSVN

## Environment Configuration

### PHP Configuration

1. **php.ini Settings**:
   ```ini
   display_errors = On
   error_reporting = E_ALL
   date.timezone = "Your/Timezone"
   memory_limit = 256M
   upload_max_filesize = 10M
   post_max_size = 10M
   ```

2. **Xdebug Configuration**:
   ```ini
   zend_extension=xdebug.so
   xdebug.remote_enable=1
   xdebug.remote_host=127.0.0.1
   xdebug.remote_port=9000
   xdebug.idekey=PHPSTORM
   ```

### Web Server Configuration

1. **Apache Configuration**:
   ```apache
   <VirtualHost *:80>
       ServerName myapp.local
       DocumentRoot /path/to/your/app/webroot
       <Directory /path/to/your/app/webroot>
           Options Indexes FollowSymLinks
           AllowOverride All
           Require all granted
       </Directory>
   </VirtualHost>
   ```

2. **Nginx Configuration**:
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

### Database Configuration

1. **MySQL Configuration**:
   ```ini
   [mysqld]
   character-set-server = utf8mb4
   collation-server = utf8mb4_unicode_ci
   ```

2. **PostgreSQL Configuration**:
   ```ini
   client_encoding = 'UTF8'
   ```

## Development Workflow

1. **Version Control Setup**:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   ```

2. **Branching Strategy**:
   - main/master: Production code
   - develop: Development code
   - feature/*: New features
   - bugfix/*: Bug fixes
   - release/*: Release preparation

3. **Development Process**:
   - Create feature branch
   - Implement changes
   - Write tests
   - Run tests
   - Create pull request
   - Code review
   - Merge to develop

## Debugging

1. **DebugKit Setup**:
   ```bash
   git clone https://github.com/cakephp/debug_kit.git app/Plugin/DebugKit
   ```

2. **Enable DebugKit**:
   ```php
   // In app/Config/bootstrap.php
   CakePlugin::load('DebugKit');
   ```

3. **Debugging Techniques**:
   - Use `debug()` function
   - Use `pr()` function
   - Use `Configure::write('debug', 2)`
   - Use Xdebug
   - Use DebugKit toolbar

## Testing

1. **PHPUnit Setup**:
   ```bash
   composer require --dev phpunit/phpunit
   ```

2. **Test Configuration**:
   ```php
   // In app/Config/bootstrap.php
   App::uses('CakeTestCase', 'TestSuite');
   ```

3. **Running Tests**:
   ```bash
   ./lib/Cake/Console/cake test app Model/Post
   ```

## Performance Optimization

1. **Cache Configuration**:
   ```php
   // In app/Config/core.php
   Configure::write('Cache.disable', false);
   ```

2. **Debug Mode**:
   ```php
   // In app/Config/core.php
   Configure::write('debug', 0);
   ```

3. **Asset Compression**:
   - Use AssetCompress plugin
   - Enable gzip compression
   - Minify CSS/JS

## Security

1. **Security Configuration**:
   ```php
   // In app/Config/core.php
   Configure::write('Security.salt', 'YOUR-SALT-HERE');
   Configure::write('Security.cipherSeed', 'YOUR-CIPHER-SEED-HERE');
   ```

2. **CSRF Protection**:
   ```php
   // In app/Controller/AppController.php
   public $components = array('Security');
   ```

3. **Input Validation**:
   - Use validation rules
   - Sanitize input
   - Use prepared statements 