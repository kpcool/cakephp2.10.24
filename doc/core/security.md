# Security

This guide covers security best practices in CakePHP 2.x.

## Authentication

1. **Basic Auth Setup**
   ```php
   // app/Controller/AppController.php
   public $components = array(
       'Auth' => array(
           'authenticate' => array('Form'),
           'authorize' => array('Controller')
       )
   );
   ```

2. **Custom Auth**
   ```php
   // app/Controller/Component/Auth/CustomAuthenticate.php
   class CustomAuthenticate extends BaseAuthenticate {
       public function authenticate(CakeRequest $request, CakeResponse $response) {
           // Custom authentication logic
       }
   }
   ```

## Authorization

1. **Controller Authorization**
   ```php
   // app/Controller/AppController.php
   public function isAuthorized($user) {
       if (isset($user['role']) && $user['role'] === 'admin') {
           return true;
       }
       return false;
   }
   ```

2. **Action Authorization**
   ```php
   // app/Controller/PostsController.php
   public function beforeFilter() {
       parent::beforeFilter();
       $this->Auth->allow('index', 'view');
       $this->Auth->deny('edit', 'delete');
   }
   ```

## CSRF Protection

1. **CSRF Component**
   ```php
   // app/Controller/AppController.php
   public $components = array('Security');
   
   public function beforeFilter() {
       parent::beforeFilter();
       $this->Security->validatePost = true;
       $this->Security->csrfCheck = true;
   }
   ```

2. **CSRF Token**
   ```php
   // app/View/Posts/add.ctp
   echo $this->Form->create('Post', array('type' => 'post'));
   echo $this->Form->input('title');
   echo $this->Form->input('body');
   echo $this->Form->end('Save Post');
   ```

## Input Validation

1. **Model Validation**
   ```php
   // app/Model/Post.php
   public $validate = array(
       'title' => array(
           'rule' => 'notEmpty',
           'message' => 'Title is required'
       ),
       'body' => array(
           'rule' => 'notEmpty',
           'message' => 'Body is required'
       )
   );
   ```

2. **Form Validation**
   ```php
   // app/View/Posts/add.ctp
   echo $this->Form->create('Post');
   echo $this->Form->input('title', array(
       'required' => true,
       'pattern' => '[A-Za-z0-9 ]+'
   ));
   echo $this->Form->input('body', array(
       'required' => true
   ));
   echo $this->Form->end('Save Post');
   ```

## XSS Prevention

1. **Output Escaping**
   ```php
   // app/View/Posts/view.ctp
   echo h($post['Post']['title']);
   echo h($post['Post']['body']);
   ```

2. **HTML Purification**
   ```php
   // app/Model/Post.php
   public function beforeSave($options = array()) {
       if (isset($this->data[$this->alias]['body'])) {
           $this->data[$this->alias]['body'] = strip_tags($this->data[$this->alias]['body']);
       }
       return true;
   }
   ```

## Best Practices

1. **Authentication**
   - Use strong passwords
   - Implement rate limiting
   - Handle session securely
   - Regular security audits

2. **Authorization**
   - Principle of least privilege
   - Role-based access control
   - Regular permission review
   - Document access rules

3. **Input Handling**
   - Validate all input
   - Sanitize data
   - Use prepared statements
   - Regular security testing

4. **Output Handling**
   - Escape all output
   - Use secure headers
   - Implement CSP
   - Regular security review 