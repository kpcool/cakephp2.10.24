# Security Configuration

This guide covers security configuration in CakePHP 2.x.

## Basic Security

1. **Security Settings**
   ```php
   // app/Config/core.php
   Configure::write('Security.salt', 'DYhG93b0qyJfIxfs2guVoUubWwvniR2G0FgaC9mi');
   Configure::write('Security.cipherSeed', '76859309657453542496749683645');
   ```

2. **Session Security**
   ```php
   // app/Config/core.php
   Configure::write('Session', array(
       'defaults' => 'php',
       'timeout' => 120,
       'cookie' => 'CAKEPHP',
       'ini' => array(
           'session.cookie_httponly' => 1,
           'session.cookie_secure' => 1
       )
   ));
   ```

## CSRF Protection

1. **CSRF Settings**
   ```php
   // app/Config/core.php
   Configure::write('Security', array(
       'csrfUseOnce' => true,
       'csrfExpires' => '+30 minutes',
       'csrfCheck' => true
   ));
   ```

2. **Form Security**
   ```php
   // In your controller
   public function beforeFilter() {
       parent::beforeFilter();
       $this->Security->requireSecure('add', 'edit');
       $this->Security->validatePost = true;
   }
   ```

## Authentication

1. **Auth Settings**
   ```php
   // app/Config/core.php
   Configure::write('Auth', array(
       'authenticate' => array('Form'),
       'authorize' => array('Controller'),
       'loginAction' => array(
           'controller' => 'users',
           'action' => 'login'
       ),
       'loginRedirect' => array(
           'controller' => 'pages',
           'action' => 'display',
           'home'
       )
   ));
   ```

2. **Password Hashing**
   ```php
   // app/Config/core.php
   Configure::write('Security', array(
       'hash' => 'sha1',
       'salt' => 'DYhG93b0qyJfIxfs2guVoUubWwvniR2G0FgaC9mi'
   ));
   ```

## Best Practices

1. **Security Design**
   - Use strong encryption
   - Implement CSRF protection
   - Secure session handling
   - Regular security updates

2. **Authentication**
   - Use strong passwords
   - Implement proper hashing
   - Regular password updates
   - Monitor login attempts

3. **Authorization**
   - Implement role-based access
   - Regular permission review
   - Monitor access logs
   - Update permissions

4. **Maintenance**
   - Regular security audits
   - Update security settings
   - Monitor security logs
   - Keep documentation current 