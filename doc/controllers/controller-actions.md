# Controller Actions

This guide covers controller actions in CakePHP 2.x.

## Standard Actions

1. **CRUD Actions**
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
       
       public function archive($year = null, $month = null) {
           $conditions = array();
           if ($year) {
               $conditions['YEAR(Post.created)'] = $year;
           }
           if ($month) {
               $conditions['MONTH(Post.created)'] = $month;
           }
           $posts = $this->Post->find('all', array(
               'conditions' => $conditions
           ));
           $this->set('posts', $posts);
       }
   }
   ```

## Action Parameters

1. **Required Parameters**
   ```php
   class PostsController extends AppController {
       public function view($id) {
           if (!$id) {
               throw new NotFoundException('Invalid post');
           }
           $post = $this->Post->findById($id);
           $this->set('post', $post);
       }
   }
   ```

2. **Optional Parameters**
   ```php
   class PostsController extends AppController {
       public function index($page = 1, $sort = 'created', $direction = 'desc') {
           $this->paginate = array(
               'limit' => 10,
               'page' => $page,
               'order' => array($sort => $direction)
           );
           $posts = $this->paginate('Post');
           $this->set('posts', $posts);
       }
   }
   ```

## Action Responses

1. **View Rendering**
   ```php
   class PostsController extends AppController {
       public function view($id) {
           $post = $this->Post->findById($id);
           $this->set('post', $post);
           $this->render('custom_view');
       }
   }
   ```

2. **Redirects**
   ```php
   class PostsController extends AppController {
       public function add() {
           if ($this->request->is('post')) {
               $this->Post->create();
               if ($this->Post->save($this->request->data)) {
                   $this->redirect(array(
                       'controller' => 'posts',
                       'action' => 'view',
                       $this->Post->id
                   ));
               }
           }
       }
   }
   ```

## Best Practices

1. **Action Design**
   - Keep actions focused
   - Use meaningful names
   - Handle errors properly
   - Follow RESTful conventions

2. **Security**
   - Validate input
   - Check permissions
   - Sanitize output
   - Use proper authentication

3. **Performance**
   - Minimize database queries
   - Use caching when appropriate
   - Optimize view rendering
   - Handle errors gracefully

4. **Maintenance**
   - Document actions
   - Keep code organized
   - Regular review
   - Update as needed 