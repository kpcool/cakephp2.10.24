# JSON and XML Views

This guide covers JSON and XML views in CakePHP 2.x.

## JSON Views

1. **Basic JSON**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->set('posts', $this->Post->find('all'));
       $this->set('_serialize', array('posts'));
   }
   ```

2. **Custom JSON**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->set('posts', $this->Post->find('all'));
       $this->set('_serialize', array('posts'));
       $this->set('_jsonp', true);
   }
   ```

## XML Views

1. **Basic XML**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->set('posts', $this->Post->find('all'));
       $this->set('_serialize', array('posts'));
       $this->RequestHandler->respondAs('xml');
   }
   ```

2. **Custom XML**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->set('posts', $this->Post->find('all'));
       $this->set('_serialize', array('posts'));
       $this->RequestHandler->respondAs('xml');
       $this->set('_xmlOptions', array('format' => 'attributes'));
   }
   ```

## Response Configuration

1. **Response Headers**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->response->header('Content-Type', 'application/json');
       $this->response->header('Cache-Control', 'no-cache');
   }
   ```

2. **Response Status**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->response->statusCode(200);
       $this->response->type('json');
   }
   ```

## Best Practices

1. **View Design**
   - Keep responses clean
   - Use meaningful data
   - Follow conventions
   - Document format

2. **Code Organization**
   - Group related views
   - Maintain consistency
   - Use inheritance
   - Version control

3. **Performance**
   - Minimize data
   - Cache responses
   - Optimize queries
   - Regular review

4. **Maintenance**
   - Update documentation
   - Test responses
   - Handle errors
   - Regular updates 