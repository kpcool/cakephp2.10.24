# Error Handling

This guide covers error handling and debugging in CakePHP 2.x.

## Configuration

1. **Error Level Configuration**
   ```php
   // app/Config/core.php
   Configure::write('Error', array(
       'handler' => 'ErrorHandler::handleError',
       'level' => E_ALL & ~E_DEPRECATED,
       'trace' => true
   ));
   ```

2. **Exception Handling**
   ```php
   // app/Config/core.php
   Configure::write('Exception', array(
       'handler' => 'ErrorHandler::handleException',
       'renderer' => 'ExceptionRenderer',
       'log' => true
   ));
   ```

## Error Handling

1. **Custom Error Handler**
   ```php
   // app/Config/bootstrap.php
   App::uses('ErrorHandler', 'Error');
   
   class AppErrorHandler extends ErrorHandler {
       public static function handleError($code, $description, $file = null, $line = null, $context = null) {
           // Custom error handling logic
           return parent::handleError($code, $description, $file, $line, $context);
       }
   }
   ```

2. **Exception Handling**
   ```php
   // app/Controller/AppController.php
   public function beforeFilter() {
       parent::beforeFilter();
       $this->set('error', $this->Session->read('Message.error'));
   }
   ```

## Debugging

1. **Debug Helper**
   ```php
   // In views
   debug($variable);
   pr($array);
   ```

2. **Logging**
   ```php
   // In controllers
   CakeLog::write('debug', 'Debug message');
   CakeLog::write('error', 'Error message');
   ```

## Error Pages

1. **Custom Error Pages**
   ```php
   // app/View/Errors/error400.ctp
   <h2><?php echo $name; ?></h2>
   <p class="error">
       <strong><?php echo __d('cake', 'Error'); ?>: </strong>
       <?php echo __d('cake', 'The requested address %s was not found on this server.', "<strong>'{$url}'</strong>"); ?>
   </p>
   ```

2. **Maintenance Mode**
   ```php
   // app/Config/core.php
   Configure::write('maintenance', false);
   
   // app/Controller/AppController.php
   public function beforeFilter() {
       if (Configure::read('maintenance')) {
           throw new MaintenanceException();
       }
   }
   ```

## Best Practices

1. **Error Handling**
   - Use appropriate error levels
   - Log all errors
   - Custom error pages
   - Regular monitoring

2. **Debugging**
   - Use debug helper
   - Log important events
   - Test error cases
   - Document errors

3. **Maintenance**
   - Regular error review
   - Update error pages
   - Monitor error logs
   - Backup error data

4. **Security**
   - Hide sensitive errors
   - Secure error logs
   - Handle exceptions
   - Regular security review 