# Database Configuration

This guide covers database configuration in CakePHP 2.x.

## Configuration Files

1. **Database Configuration**
   ```php
   // app/Config/database.php
   class DATABASE_CONFIG {
       public $default = array(
           'datasource' => 'Database/Mysql',
           'persistent' => false,
           'host' => 'localhost',
           'login' => 'user',
           'password' => 'password',
           'database' => 'database_name',
           'prefix' => '',
           'encoding' => 'utf8'
       );
       
       public $test = array(
           'datasource' => 'Database/Mysql',
           'persistent' => false,
           'host' => 'localhost',
           'login' => 'user',
           'password' => 'password',
           'database' => 'test_database',
           'prefix' => '',
           'encoding' => 'utf8'
       );
   }
   ```

2. **Multiple Database Connections**
   ```php
   class Post extends AppModel {
       public $useDbConfig = 'alternate';
   }
   ```

## Supported Databases

1. **MySQL/MariaDB**
   ```php
   'datasource' => 'Database/Mysql',
   'encoding' => 'utf8'
   ```

2. **PostgreSQL**
   ```php
   'datasource' => 'Database/Postgres',
   'encoding' => 'utf8'
   ```

3. **SQLite**
   ```php
   'datasource' => 'Database/Sqlite',
   'database' => 'path/to/database.sqlite'
   ```

4. **SQL Server**
   ```php
   'datasource' => 'Database/Sqlserver',
   'encoding' => 'utf8'
   ```

## Connection Options

1. **Basic Options**
   - `datasource`: Database type
   - `persistent`: Persistent connection
   - `host`: Database server
   - `login`: Username
   - `password`: Password
   - `database`: Database name
   - `prefix`: Table prefix
   - `encoding`: Character encoding

2. **Advanced Options**
   - `port`: Custom port
   - `schema`: Schema name
   - `unix_socket`: Unix socket path
   - `settings`: Additional settings

## Best Practices

1. **Security**
   - Use environment variables for credentials
   - Implement proper access control
   - Use SSL for remote connections
   - Regular backups

2. **Performance**
   - Use persistent connections
   - Implement connection pooling
   - Optimize query caching
   - Proper indexing

3. **Maintenance**
   - Regular backups
   - Monitor performance
   - Update database software
   - Clean up old data

4. **Development**
   - Use separate databases for development
   - Implement database migrations
   - Use version control
   - Document schema changes 