# Controller Callbacks

This guide covers controller callbacks in CakePHP 2.x.

## Callback Types

1. **Before Callbacks**
   ```php
   class PostsController extends AppController {
       public function beforeFilter() {
           parent::beforeFilter();
           // Code to run before any controller action
       }
       
       public function beforeRender() {
           // Code to run before view rendering
       }
   }
   ```

2. **After Callbacks**
   ```php
   class PostsController extends AppController {
       public function afterFilter() {
           // Code to run after any controller action
       }
   }
   ```

## Common Callbacks

1. **beforeFilter**
   ```php
   class PostsController extends AppController {
       public function beforeFilter() {
           parent::beforeFilter();
           $this->Auth->allow('index', 'view');
           $this->Security->requireSecure('add', 'edit');
       }
   }
   ```

2. **beforeRender**
   ```php
   class PostsController extends AppController {
       public function beforeRender() {
           $this->set('currentUser', $this->Auth->user());
           $this->set('isAdmin', $this->Auth->user('role') === 'admin');
       }
   }
   ```

3. **afterFilter**
   ```php
   class PostsController extends AppController {
       public function afterFilter() {
           // Log action completion
           $this->log("Action {$this->action} completed", 'info');
       }
   }
   ```

## Working with Callbacks

1. **Callback Order**
   ```php
   class PostsController extends AppController {
       public function beforeFilter() {
           parent::beforeFilter();
           // Runs first
       }
       
       public function beforeRender() {
           // Runs before view rendering
       }
       
       public function afterFilter() {
           // Runs last
       }
   }
   ```

2. **Conditional Callbacks**
   ```php
   class PostsController extends AppController {
       public function beforeFilter() {
           parent::beforeFilter();
           if ($this->action === 'add' || $this->action === 'edit') {
               $this->Security->requireSecure();
           }
       }
   }
   ```

## Best Practices

1. **Callback Design**
   - Keep callbacks focused
   - Document callback purpose
   - Consider performance impact
   - Handle errors properly

2. **Security**
   - Validate in beforeFilter
   - Check permissions early
   - Sanitize data
   - Handle errors

3. **Performance**
   - Minimize callback logic
   - Cache when appropriate
   - Optimize queries
   - Consider timing

4. **Maintenance**
   - Document callbacks
   - Keep callbacks simple
   - Regular review
   - Update as needed 