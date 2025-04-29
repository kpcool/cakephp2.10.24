# Core Configuration

This guide covers core configuration settings in CakePHP 2.x.

## Application Settings

1. **Basic Settings**
   ```php
   // app/Config/core.php
   Configure::write('App.baseUrl', '/myapp');
   Configure::write('App.encoding', 'UTF-8');
   Configure::write('App.defaultLocale', 'en_US');
   Configure::write('App.defaultTimezone', 'UTC');
   ```

2. **Debug Settings**
   ```php
   // app/Config/core.php
   Configure::write('debug', 2); // 0: production, 1: development, 2: debug
   Configure::write('Error', array(
       'handler' => 'ErrorHandler::handleError',
       'level' => E_ALL & ~E_DEPRECATED,
       'trace' => true
   ));
   ```

## Routing Configuration

1. **Basic Routing**
   ```php
   // app/Config/routes.php
   Router::connect('/', array('controller' => 'pages', 'action' => 'display', 'home'));
   Router::connect('/pages/*', array('controller' => 'pages', 'action' => 'display'));
   ```

2. **Custom Routes**
   ```php
   // app/Config/routes.php
   Router::connect(
       '/blog/:year/:month/:day/:slug',
       array('controller' => 'posts', 'action' => 'view'),
       array(
           'pass' => array('year', 'month', 'day', 'slug'),
           'year' => '[12][0-9]{3}',
           'month' => '[01][0-9]',
           'day' => '[0-3][0-9]'
       )
   );
   ```

## Session Configuration

1. **Session Settings**
   ```php
   // app/Config/core.php
   Configure::write('Session', array(
       'defaults' => 'php',
       'timeout' => 120,
       'cookie' => 'CAKEPHP',
       'ini' => array(
           'session.cookie_httponly' => 1
       )
   ));
   ```

2. **Security Settings**
   ```php
   // app/Config/core.php
   Configure::write('Security.salt', 'DYhG93b0qyJfIxfs2guVoUubWwvniR2G0FgaC9mi');
   Configure::write('Security.cipherSeed', '76859309657453542496749683645');
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