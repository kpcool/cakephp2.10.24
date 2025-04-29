# Controllers

This guide covers the Controller layer in CakePHP 2.x, which handles application flow and business logic.

## Controller Basics

1. **Creating Controllers**
   ```php
   class PostsController extends AppController {
       public $name = 'Posts';
       public $uses = array('Post', 'Comment');
       public $components = array('Session', 'Auth');
       public $helpers = array('Html', 'Form');
   }
   ```

2. **Controller Actions**
   ```php
   class PostsController extends AppController {
       public function index() {
           $posts = $this->Post->find('all');
           $this->set('posts', $posts);
       }
       
       public function view($id = null) {
           $post = $this->Post->findById($id);
           $this->set('post', $post);
       }
   }
   ```

3. **Request Handling**
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

## Request and Response

1. **Request Data**
   ```php
   class PostsController extends AppController {
       public function add() {
           // Get POST data
           $postData = $this->request->data;
           
           // Get query parameters
           $page = $this->request->query('page');
           
           // Get named parameters
           $id = $this->request->params['named']['id'];
       }
   }
   ```

2. **Response Handling**
   ```php
   class PostsController extends AppController {
       public function download() {
           $this->response->file('path/to/file.pdf');
           return $this->response;
       }
       
       public function json() {
           $this->response->type('json');
           $this->set('_serialize', array('data'));
       }
   }
   ```

## Components

1. **Using Components**
   ```php
   class PostsController extends AppController {
       public $components = array(
           'Session',
           'Auth' => array(
               'loginAction' => array(
                   'controller' => 'users',
                   'action' => 'login'
               )
           )
       );
   }
   ```

2. **Common Components**
   - Auth: Authentication and authorization
   - Session: Session handling
   - Security: Security features
   - RequestHandler: Request type handling
   - Paginator: Pagination
   - Flash: Flash messages

## Controller Callbacks

1. **Before Callbacks**
   ```php
   class PostsController extends AppController {
       public function beforeFilter() {
           parent::beforeFilter();
           $this->Auth->allow('index', 'view');
       }
   }
   ```

2. **After Callbacks**
   ```php
   class PostsController extends AppController {
       public function afterFilter() {
           // Perform cleanup
       }
   }
   ```

3. **Common Callbacks**
   - beforeFilter
   - beforeRender
   - afterFilter
   - beforeRedirect

## View Integration

1. **Setting View Variables**
   ```php
   class PostsController extends AppController {
       public function view($id) {
           $post = $this->Post->findById($id);
           $this->set('post', $post);
           $this->set('title', $post['Post']['title']);
       }
   }
   ```

2. **View Selection**
   ```php
   class PostsController extends AppController {
       public function view($id) {
           $this->render('custom_view');
       }
   }
   ```

## Error Handling

1. **Error Actions**
   ```php
   class PostsController extends AppController {
       public function error404() {
           $this->response->statusCode(404);
       }
   }
   ```

2. **Exception Handling**
   ```php
   class PostsController extends AppController {
       public function view($id) {
           try {
               $post = $this->Post->findById($id);
               if (!$post) {
                   throw new NotFoundException('Post not found');
               }
               $this->set('post', $post);
           } catch (Exception $e) {
               $this->Session->setFlash($e->getMessage());
               $this->redirect(array('action' => 'index'));
           }
       }
   }
   ```

## Best Practices

1. **Code Organization**
   - Keep controllers thin
   - Move business logic to models
   - Use components for shared functionality
   - Follow RESTful conventions

2. **Security**
   - Validate all input
   - Use proper authentication
   - Implement CSRF protection
   - Sanitize output

3. **Performance**
   - Minimize database queries
   - Use caching when appropriate
   - Optimize view rendering
   - Handle errors gracefully

4. **Maintainability**
   - Use meaningful action names
   - Document complex logic
   - Follow naming conventions
   - Keep actions focused 