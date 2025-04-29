# Request Handling

This guide covers request handling in CakePHP 2.x controllers.

## Request Data

1. **Accessing Request Data**
   ```php
   class PostsController extends AppController {
       public function add() {
           // Get POST data
           $postData = $this->request->data;
           
           // Get query parameters
           $page = $this->request->query('page');
           
           // Get named parameters
           $id = $this->request->params['named']['id'];
           
           // Get passed arguments
           $id = $this->request->params['pass'][0];
       }
   }
   ```

2. **Request Methods**
   ```php
   class PostsController extends AppController {
       public function add() {
           if ($this->request->is('post')) {
               // Handle POST request
           }
           
           if ($this->request->is('get')) {
               // Handle GET request
           }
           
           if ($this->request->is('ajax')) {
               // Handle AJAX request
           }
       }
   }
   ```

## Request Parameters

1. **URL Parameters**
   ```php
   class PostsController extends AppController {
       public function view($id = null) {
           // Get URL parameters
           $id = $this->request->params['id'];
           $slug = $this->request->params['slug'];
           
           // Get controller/action
           $controller = $this->request->params['controller'];
           $action = $this->request->params['action'];
       }
   }
   ```

2. **Query Parameters**
   ```php
   class PostsController extends AppController {
       public function index() {
           // Get query parameters
           $page = $this->request->query('page');
           $sort = $this->request->query('sort');
           $direction = $this->request->query('direction');
           
           // Get all query parameters
           $query = $this->request->query;
       }
   }
   ```

## Request Types

1. **Form Submissions**
   ```php
   class PostsController extends AppController {
       public function add() {
           if ($this->request->is('post')) {
               $this->Post->create();
               if ($this->Post->save($this->request->data)) {
                   $this->Session->setFlash('Post saved successfully');
                   $this->redirect(array('action' => 'index'));
               }
           }
       }
   }
   ```

2. **AJAX Requests**
   ```php
   class PostsController extends AppController {
       public function search() {
           if ($this->request->is('ajax')) {
               $query = $this->request->data['query'];
               $posts = $this->Post->find('all', array(
                   'conditions' => array('Post.title LIKE' => "%$query%")
               ));
               $this->set('posts', $posts);
               $this->layout = 'ajax';
           }
       }
   }
   ```

## Request Validation

1. **Input Validation**
   ```php
   class PostsController extends AppController {
       public function add() {
           if ($this->request->is('post')) {
               $this->Post->set($this->request->data);
               if ($this->Post->validates()) {
                   // Data is valid
               } else {
                   $errors = $this->Post->validationErrors;
               }
           }
       }
   }
   ```

2. **Security Validation**
   ```php
   class PostsController extends AppController {
       public function beforeFilter() {
           parent::beforeFilter();
           $this->Security->validatePost = true;
           $this->Security->csrfCheck = true;
       }
   }
   ```

## Best Practices

1. **Request Handling**
   - Validate all input
   - Sanitize data
   - Check request methods
   - Handle errors properly

2. **Security**
   - Use CSRF protection
   - Validate input
   - Check permissions
   - Sanitize output

3. **Performance**
   - Minimize request data
   - Use proper caching
   - Optimize queries
   - Handle errors gracefully

4. **Maintenance**
   - Document request handling
   - Keep code organized
   - Regular review
   - Update as needed 