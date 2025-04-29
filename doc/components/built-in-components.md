# Built-in Components

This guide covers the built-in components in CakePHP 2.x.

## Authentication

1. **Auth Component**
   ```php
   // In controller
   public $components = array(
       'Auth' => array(
           'authenticate' => array('Form'),
           'authorize' => array('Controller')
       )
   );
   ```

2. **Acl Component**
   ```php
   // In controller
   public $components = array('Acl');
   
   public function checkAccess() {
       $this->Acl->check($user, 'controller/action');
   }
   ```

## Session & Request

1. **Session Component**
   ```php
   // In controller
   public $components = array('Session');
   
   public function method() {
       $this->Session->write('key', 'value');
       $value = $this->Session->read('key');
   }
   ```

2. **RequestHandler Component**
   ```php
   // In controller
   public $components = array('RequestHandler');
   
   public function method() {
       if ($this->RequestHandler->isAjax()) {
           // Handle AJAX request
       }
   }
   ```

## Security

1. **Security Component**
   ```php
   // In controller
   public $components = array('Security');
   
   public function beforeFilter() {
       $this->Security->requireSecure();
   }
   ```

2. **Csrf Component**
   ```php
   // In controller
   public $components = array('Csrf');
   
   public function beforeFilter() {
       $this->Csrf->validatePost();
   }
   ```

## Pagination & Flash

1. **Paginator Component**
   ```php
   // In controller
   public $components = array('Paginator');
   
   public function index() {
       $this->Paginator->settings = array(
           'limit' => 10,
           'order' => array('created' => 'desc')
       );
       $data = $this->Paginator->paginate('Model');
   }
   ```

2. **Flash Component**
   ```php
   // In controller
   public $components = array('Flash');
   
   public function method() {
       $this->Flash->success('Operation successful');
       $this->Flash->error('Operation failed');
   }
   ```

## Best Practices

1. **Component Usage**
   - Understand purpose
   - Configure properly
   - Handle errors
   - Test thoroughly

2. **Security**
   - Validate input
   - Sanitize data
   - Handle sessions
   - Regular audits

3. **Performance**
   - Optimize settings
   - Cache data
   - Monitor usage
   - Regular review

4. **Maintenance**
   - Update settings
   - Monitor logs
   - Backup data
   - Regular updates 