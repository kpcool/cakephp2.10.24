# View Basics

This guide covers the fundamentals of views in CakePHP 2.x.

## Basic View Structure

1. **View File**
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

2. **View Variables**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->set('posts', $this->Post->find('all'));
       $this->set('title', 'Blog Posts');
   }
   ```

## View Rendering

1. **Basic Rendering**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->render('index');
   }
   ```

2. **Custom Rendering**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->render('custom_view');
       $this->render('custom_view', 'custom_layout');
   }
   ```

## View Helpers

1. **Helper Usage**
   ```php
   // app/View/Posts/index.ctp
   echo $this->Html->link('Home', '/');
   echo $this->Form->create('Post');
   echo $this->Session->flash();
   ```

2. **Helper Configuration**
   ```php
   // app/Controller/PostsController.php
   public $helpers = array('Html', 'Form', 'Session');
   ```

## Best Practices

1. **View Organization**
   - Keep views focused
   - Use meaningful names
   - Follow conventions
   - Document views

2. **Code Structure**
   - Separate logic
   - Use helpers
   - Maintain consistency
   - Version control

3. **Performance**
   - Minimize processing
   - Cache output
   - Optimize queries
   - Regular review

4. **Maintenance**
   - Update documentation
   - Test thoroughly
   - Handle errors
   - Regular updates 