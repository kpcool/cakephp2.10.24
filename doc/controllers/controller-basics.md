# Controller Basics

This guide covers the fundamental concepts of Controllers in CakePHP 2.x.

## Creating Controllers

1. **Basic Controller Structure**
   ```php
   class PostsController extends AppController {
       public $name = 'Posts';
       public $uses = array('Post', 'Comment');
       public $components = array('Session', 'Auth');
       public $helpers = array('Html', 'Form');
   }
   ```

2. **Controller Properties**
   - `$name`: Controller name
   - `$uses`: Models to use
   - `$components`: Components to load
   - `$helpers`: Helpers to load
   - `$layout`: Default layout
   - `$autoRender`: Auto render views

## Basic Actions

1. **Standard CRUD Actions**
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
       
       public function add() {
           if ($this->request->is('post')) {
               $this->Post->create();
               if ($this->Post->save($this->request->data)) {
                   $this->Session->setFlash('Post saved successfully');
                   $this->redirect(array('action' => 'index'));
               }
           }
       }
       
       public function edit($id = null) {
           $this->Post->id = $id;
           if ($this->request->is('post') || $this->request->is('put')) {
               if ($this->Post->save($this->request->data)) {
                   $this->Session->setFlash('Post updated successfully');
                   $this->redirect(array('action' => 'index'));
               }
           }
           $this->request->data = $this->Post->findById($id);
       }
       
       public function delete($id = null) {
           if ($this->Post->delete($id)) {
               $this->Session->setFlash('Post deleted successfully');
               $this->redirect(array('action' => 'index'));
           }
       }
   }
   ```

2. **Custom Actions**
   ```php
   class PostsController extends AppController {
       public function search() {
           if ($this->request->is('post')) {
               $query = $this->request->data['Post']['query'];
               $posts = $this->Post->find('all', array(
                   'conditions' => array('Post.title LIKE' => "%$query%")
               ));
               $this->set('posts', $posts);
           }
       }
   }
   ```

## Controller Configuration

1. **Component Configuration**
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

2. **Helper Configuration**
   ```php
   class PostsController extends AppController {
       public $helpers = array(
           'Html',
           'Form',
           'Time' => array('format' => 'Y-m-d')
       );
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