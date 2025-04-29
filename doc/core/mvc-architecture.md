# MVC Architecture

This guide covers the Model-View-Controller (MVC) architecture in CakePHP 2.x.

## Model Layer

1. **Basic Model**
   ```php
   // app/Model/Post.php
   class Post extends AppModel {
       public $name = 'Post';
       public $validate = array(
           'title' => array(
               'rule' => 'notEmpty'
           )
       );
       
       public $hasMany = array('Comment');
   }
   ```

2. **Model Associations**
   ```php
   // app/Model/Post.php
   public $belongsTo = array('User');
   public $hasMany = array('Comment');
   public $hasAndBelongsToMany = array('Tag');
   ```

## Controller Layer

1. **Basic Controller**
   ```php
   // app/Controller/PostsController.php
   class PostsController extends AppController {
       public $components = array('Session');
       
       public function index() {
           $this->set('posts', $this->Post->find('all'));
       }
       
       public function view($id = null) {
           $this->Post->id = $id;
           $this->set('post', $this->Post->read());
       }
   }
   ```

2. **Controller Actions**
   ```php
   // app/Controller/PostsController.php
   public function add() {
       if ($this->request->is('post')) {
           if ($this->Post->save($this->request->data)) {
               $this->Session->setFlash('Post saved.');
               $this->redirect(array('action' => 'index'));
           }
       }
   }
   ```

## View Layer

1. **Basic View**
   ```php
   // app/View/Posts/index.ctp
   <h1>Blog Posts</h1>
   <table>
       <tr>
           <th>Title</th>
           <th>Created</th>
       </tr>
       <?php foreach ($posts as $post): ?>
       <tr>
           <td><?php echo $post['Post']['title']; ?></td>
           <td><?php echo $post['Post']['created']; ?></td>
       </tr>
       <?php endforeach; ?>
   </table>
   ```

2. **View Elements**
   ```php
   // app/View/Elements/navigation.ctp
   <ul>
       <li><?php echo $this->Html->link('Home', '/'); ?></li>
       <li><?php echo $this->Html->link('About', '/about'); ?></li>
   </ul>
   ```

## Request Flow

1. **Request Handling**
   ```
   Request -> Router -> Controller -> Model -> View -> Response
   ```

2. **Component Flow**
   ```php
   // app/Controller/AppController.php
   public function beforeFilter() {
       // Before controller action
   }
   
   public function afterFilter() {
       // After controller action
   }
   ```

## Best Practices

1. **Model Layer**
   - Keep business logic in models
   - Use appropriate associations
   - Validate data
   - Document relationships

2. **Controller Layer**
   - Keep controllers thin
   - Use components
   - Handle requests
   - Manage sessions

3. **View Layer**
   - Separate presentation logic
   - Use helpers
   - Create reusable elements
   - Maintain consistency

4. **Architecture**
   - Follow MVC pattern
   - Use conventions
   - Document code
   - Regular review 