# View Variables

This guide covers view variables in CakePHP 2.x.

## Setting Variables

1. **Basic Variables**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->set('posts', $this->Post->find('all'));
       $this->set('title', 'Blog Posts');
   }
   ```

2. **Multiple Variables**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->set(array(
           'posts' => $this->Post->find('all'),
           'title' => 'Blog Posts',
           'count' => $this->Post->find('count')
       ));
   }
   ```

## Variable Types

1. **Model Data**
   ```php
   // app/Controller/PostsController.php
   public function view($id) {
       $this->set('post', $this->Post->findById($id));
       $this->set('comments', $this->Post->Comment->find('all', array(
           'conditions' => array('Comment.post_id' => $id)
       )));
   }
   ```

2. **Helper Data**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->set('pagination', array(
           'limit' => 10,
           'page' => 1
       ));
   }
   ```

## Variable Usage

1. **View Access**
   ```php
   // app/View/Posts/index.ctp
   <h1><?php echo $title; ?></h1>
   <?php foreach ($posts as $post): ?>
       <h2><?php echo $post['Post']['title']; ?></h2>
   <?php endforeach; ?>
   ```

2. **Helper Access**
   ```php
   // app/View/Helper/CustomHelper.php
   public function formatData() {
       $posts = $this->_View->viewVars['posts'];
       // Process posts
   }
   ```

## Best Practices

1. **Variable Design**
   - Use meaningful names
   - Document variables
   - Follow conventions
   - Regular review

2. **Code Organization**
   - Group related variables
   - Maintain consistency
   - Use inheritance
   - Version control

3. **Performance**
   - Minimize variables
   - Cache data
   - Optimize queries
   - Regular review

4. **Maintenance**
   - Update documentation
   - Test variables
   - Handle errors
   - Regular updates 