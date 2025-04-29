# Request and Response

This guide covers request and response handling in CakePHP 2.x.

## Request Object

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

## Response Object

1. **Setting Response Headers**
   ```php
   class PostsController extends AppController {
       public function download() {
           $this->response->type('application/pdf');
           $this->response->download('document.pdf');
       }
   }
   ```

2. **Custom Response Types**
   ```php
   class PostsController extends AppController {
       public function json() {
           $this->response->type('json');
           $this->set('_serialize', array('data'));
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

## Response Types

1. **JSON Response**
   ```php
   class PostsController extends AppController {
       public function api() {
           $this->response->type('json');
           $this->set('_serialize', array('data'));
           $this->set('data', array(
               'status' => 'success',
               'message' => 'Data retrieved successfully'
           ));
       }
   }
   ```

2. **File Download**
   ```php
   class PostsController extends AppController {
       public function download() {
           $this->response->type('application/pdf');
           $this->response->download('document.pdf');
           $this->response->body(file_get_contents('path/to/document.pdf'));
       }
   }
   ```

## Best Practices

1. **Request Handling**
   - Validate all input
   - Sanitize data
   - Check request methods
   - Handle errors properly

2. **Response Handling**
   - Set appropriate headers
   - Use correct content types
   - Handle errors gracefully
   - Consider caching

3. **Security**
   - Validate input
   - Sanitize output
   - Check permissions
   - Use proper authentication

4. **Performance**
   - Minimize request data
   - Use proper caching
   - Optimize responses
   - Handle errors gracefully 