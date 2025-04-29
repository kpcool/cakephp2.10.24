# Controller Components

This guide covers controller components in CakePHP 2.x.

## Component Basics

1. **Loading Components**
   ```php
   class PostsController extends AppController {
       public $components = array(
           'Auth',
           'Session',
           'RequestHandler',
           'Security'
       );
   }
   ```

2. **Component Configuration**
   ```php
   class PostsController extends AppController {
       public $components = array(
           'Auth' => array(
               'authenticate' => array('Form'),
               'authorize' => array('Controller')
           ),
           'Session' => array(
               'timeout' => 120
           )
       );
   }
   ```

## Common Components

1. **Auth Component**
   ```php
   class PostsController extends AppController {
       public $components = array('Auth');
       
       public function beforeFilter() {
           parent::beforeFilter();
           $this->Auth->allow('index', 'view');
           $this->Auth->deny('add', 'edit', 'delete');
       }
   }
   ```

2. **Session Component**
   ```php
   class PostsController extends AppController {
       public $components = array('Session');
       
       public function add() {
           if ($this->request->is('post')) {
               if ($this->Post->save($this->request->data)) {
                   $this->Session->setFlash('Post saved successfully');
                   return $this->redirect(array('action' => 'index'));
               }
               $this->Session->setFlash('Error saving post');
           }
       }
   }
   ```

3. **RequestHandler Component**
   ```php
   class PostsController extends AppController {
       public $components = array('RequestHandler');
       
       public function view($id) {
           $post = $this->Post->findById($id);
           if ($this->request->is('ajax')) {
               $this->set(compact('post'));
               $this->render('view_ajax');
           }
       }
   }
   ```

## Custom Components

1. **Creating Components**
   ```php
   // app/Controller/Component/CustomComponent.php
   class CustomComponent extends Component {
       public function initialize(Controller $controller) {
           $this->controller = $controller;
       }
       
       public function customMethod() {
           // Component logic
       }
   }
   ```

2. **Using Custom Components**
   ```php
   class PostsController extends AppController {
       public $components = array('Custom');
       
       public function someAction() {
           $this->Custom->customMethod();
       }
   }
   ```

## Best Practices

1. **Component Design**
   - Keep components focused
   - Document component purpose
   - Consider reusability
   - Handle errors properly

2. **Security**
   - Validate component data
   - Check permissions
   - Sanitize input
   - Handle errors

3. **Performance**
   - Minimize component logic
   - Cache when appropriate
   - Optimize queries
   - Consider timing

4. **Maintenance**
   - Document components
   - Keep components simple
   - Regular review
   - Update as needed 