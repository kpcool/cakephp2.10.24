# Environment Configuration

This guide covers environment configuration in CakePHP 2.x.

## Environment Setup

1. **Development Environment**
   ```php
   // app/Config/bootstrap.php
   Configure::write('debug', 2);
   Configure::write('Cache.disable', true);
   Configure::write('Error', array(
       'handler' => 'ErrorHandler::handleError',
       'level' => E_ALL & ~E_DEPRECATED,
       'trace' => true
   ));
   ```

2. **Production Environment**
   ```php
   // app/Config/bootstrap.php
   Configure::write('debug', 0);
   Configure::write('Cache.disable', false);
   Configure::write('Error', array(
       'handler' => 'ErrorHandler::handleError',
       'level' => E_ALL & ~E_DEPRECATED,
       'trace' => false
   ));
   ```

## Environment Variables

1. **Setting Variables**
   ```php
   // app/Config/bootstrap.php
   $env = getenv('CAKE_ENV') ?: 'development';
   
   if ($env === 'development') {
       Configure::write('debug', 2);
       Configure::write('Cache.disable', true);
   } else {
       Configure::write('debug', 0);
       Configure::write('Cache.disable', false);
   }
   ```

2. **Using Variables**
   ```php
   // app/Config/database.php
   class DATABASE_CONFIG {
       public $default = array(
           'datasource' => 'Database/Mysql',
           'persistent' => false,
           'host' => getenv('DB_HOST') ?: 'localhost',
           'login' => getenv('DB_USER') ?: 'user',
           'password' => getenv('DB_PASS') ?: 'password',
           'database' => getenv('DB_NAME') ?: 'myapp',
           'prefix' => '',
           'encoding' => 'utf8'
       );
   }
   ```

## Environment-Specific Settings

1. **Development Settings**
   ```php
   // app/Config/environments/development.php
   Configure::write('debug', 2);
   Configure::write('Cache.disable', true);
   Configure::write('Error', array(
       'handler' => 'ErrorHandler::handleError',
       'level' => E_ALL & ~E_DEPRECATED,
       'trace' => true
   ));
   ```

2. **Production Settings**
   ```php
   // app/Config/environments/production.php
   Configure::write('debug', 0);
   Configure::write('Cache.disable', false);
   Configure::write('Error', array(
       'handler' => 'ErrorHandler::handleError',
       'level' => E_ALL & ~E_DEPRECATED,
       'trace' => false
   ));
   ```

## Best Practices

1. **Environment Design**
   - Use environment variables
   - Separate configurations
   - Document settings
   - Keep sensitive data secure

2. **Security**
   - Protect credentials
   - Use environment variables
   - Validate settings
   - Regular security review

3. **Performance**
   - Optimize settings
   - Use proper caching
   - Monitor performance
   - Regular maintenance

4. **Maintenance**
   - Document changes
   - Version control
   - Regular review
   - Update as needed 