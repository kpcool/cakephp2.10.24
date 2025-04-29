# Database Configuration

This guide covers database configuration in CakePHP 2.x.

## Connection Settings

1. **Basic Configuration**
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

2. **Multiple Connections**
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
       
       public $test = array(
           'datasource' => 'Database/Mysql',
           'persistent' => false,
           'host' => 'localhost',
           'login' => 'test_user',
           'password' => 'test_password',
           'database' => 'myapp_test',
           'prefix' => '',
           'encoding' => 'utf8'
       );
   }
   ```

## DataSource Configuration

1. **MySQL Configuration**
   ```php
   // app/Config/database.php
   public $default = array(
       'datasource' => 'Database/Mysql',
       'persistent' => false,
       'host' => 'localhost',
       'login' => 'user',
       'password' => 'password',
       'database' => 'myapp',
       'prefix' => '',
       'encoding' => 'utf8',
       'port' => '3306'
   );
   ```

2. **PostgreSQL Configuration**
   ```php
   // app/Config/database.php
   public $default = array(
       'datasource' => 'Database/Postgres',
       'persistent' => false,
       'host' => 'localhost',
       'login' => 'user',
       'password' => 'password',
       'database' => 'myapp',
       'prefix' => '',
       'encoding' => 'utf8',
       'port' => '5432'
   );
   ```

## Environment Configuration

1. **Development Environment**
   ```php
   // app/Config/database.php
   public $default = array(
       'datasource' => 'Database/Mysql',
       'persistent' => false,
       'host' => 'localhost',
       'login' => 'dev_user',
       'password' => 'dev_password',
       'database' => 'myapp_dev',
       'prefix' => '',
       'encoding' => 'utf8'
   );
   ```

2. **Production Environment**
   ```php
   // app/Config/database.php
   public $default = array(
       'datasource' => 'Database/Mysql',
       'persistent' => false,
       'host' => 'prod_host',
       'login' => 'prod_user',
       'password' => 'prod_password',
       'database' => 'myapp_prod',
       'prefix' => '',
       'encoding' => 'utf8'
   );
   ```

## Best Practices

1. **Configuration Design**
   - Use environment variables
   - Separate credentials
   - Document connections
   - Keep sensitive data secure

2. **Security**
   - Protect credentials
   - Use strong passwords
   - Limit database access
   - Regular security review

3. **Performance**
   - Optimize connections
   - Use connection pooling
   - Monitor performance
   - Regular maintenance

4. **Maintenance**
   - Document changes
   - Version control
   - Regular backup
   - Update as needed 