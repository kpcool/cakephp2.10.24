# Configuration Basics

This guide covers the basic configuration concepts in CakePHP 2.x.

## Configuration Files

1. **Core Configuration**
   ```php
   // app/Config/core.php
   Configure::write('App.baseUrl', '/myapp');
   Configure::write('App.encoding', 'UTF-8');
   Configure::write('App.defaultLocale', 'en_US');
   ```

2. **Database Configuration**
   ```php
   // app/Config/database.php
   class DATABASE_CONFIG {
       public $default = array(
           'datasource' => 'Database/Mysql',
           'persistent' => false,
           'host' => 'localhost',
           'login' => 'user',
           'password' => 'password',
           'database' => 'myapp',
           'prefix' => '',
           'encoding' => 'utf8'
       );
   }
   ```

## Configuration Methods

1. **Writing Configuration**
   ```php
   // Write a single value
   Configure::write('App.baseUrl', '/myapp');
   
   // Write multiple values
   Configure::write('App', array(
       'baseUrl' => '/myapp',
       'encoding' => 'UTF-8'
   ));
   ```

2. **Reading Configuration**
   ```php
   // Read a single value
   $baseUrl = Configure::read('App.baseUrl');
   
   // Read all values
   $appConfig = Configure::read('App');
   ```

## Environment Configuration

1. **Development Environment**
   ```php
   // app/Config/bootstrap.php
   Configure::write('debug', 2);
   Configure::write('Cache.disable', true);
   ```

2. **Production Environment**
   ```php
   // app/Config/bootstrap.php
   Configure::write('debug', 0);
   Configure::write('Cache.disable', false);
   ```

## Best Practices

1. **Configuration Design**
   - Use meaningful names
   - Group related settings
   - Document configurations
   - Keep sensitive data secure

2. **Security**
   - Protect sensitive data
   - Use environment variables
   - Validate configuration
   - Regular security review

3. **Performance**
   - Cache configurations
   - Minimize dynamic config
   - Optimize settings
   - Monitor impact

4. **Maintenance**
   - Document changes
   - Version control
   - Regular review
   - Update as needed 