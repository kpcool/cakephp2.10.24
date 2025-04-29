# Logging Configuration

This guide covers logging configuration in CakePHP 2.x.

## Basic Logging

1. **Log Configuration**
   ```php
   // app/Config/bootstrap.php
   CakeLog::config('default', array(
       'engine' => 'File',
       'path' => LOGS,
       'file' => 'debug.log',
       'types' => array('notice', 'info', 'debug'),
       'scopes' => false
   ));
   ```

2. **Multiple Log Configs**
   ```php
   // app/Config/bootstrap.php
   CakeLog::config('error', array(
       'engine' => 'File',
       'path' => LOGS,
       'file' => 'error.log',
       'types' => array('error', 'warning'),
       'scopes' => false
   ));
   
   CakeLog::config('debug', array(
       'engine' => 'File',
       'path' => LOGS,
       'file' => 'debug.log',
       'types' => array('notice', 'info', 'debug'),
       'scopes' => false
   ));
   ```

## Log Levels

1. **Error Logging**
   ```php
   // In your code
   CakeLog::error('Error message');
   CakeLog::warning('Warning message');
   ```

2. **Debug Logging**
   ```php
   // In your code
   CakeLog::debug('Debug message');
   CakeLog::info('Info message');
   CakeLog::notice('Notice message');
   ```

## Custom Logging

1. **Custom Log Engine**
   ```php
   // app/Lib/Log/MyCustomLog.php
   App::uses('BaseLog', 'Log/Engine');
   
   class MyCustomLog extends BaseLog {
       public function write($type, $message) {
           // Custom logging logic
       }
   }
   ```

2. **Using Custom Engine**
   ```php
   // app/Config/bootstrap.php
   CakeLog::config('custom', array(
       'engine' => 'MyCustomLog',
       'types' => array('error', 'warning', 'info'),
       'scopes' => false
   ));
   ```

## Best Practices

1. **Log Design**
   - Use appropriate levels
   - Include context
   - Format consistently
   - Consider log size

2. **Performance**
   - Monitor log size
   - Rotate logs
   - Use appropriate levels
   - Regular maintenance

3. **Security**
   - Protect log files
   - Sanitize log data
   - Monitor log access
   - Regular security review

4. **Maintenance**
   - Regular log rotation
   - Monitor log size
   - Update configurations
   - Document changes