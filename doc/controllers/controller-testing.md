# Controller Testing

This guide covers testing controllers in CakePHP 2.x.

## Basic Testing

1. **Controller Test Setup**
   ```php
   // app/Test/Case/Controller/PostsControllerTest.php
   App::uses('PostsController', 'Controller');
   
   class PostsControllerTest extends ControllerTestCase {
       public $fixtures = array(
           'app.post',
           'app.user',
           'app.comment'
       );
       
       public function setUp() {
           parent::setUp();
           $this->Posts = $this->generate('Posts');
       }
   }
   ```

2. **Basic Action Test**
   ```php
   class PostsControllerTest extends ControllerTestCase {
       public function testIndex() {
           $result = $this->testAction('/posts/index');
           $this->assertContains('posts', $result);
       }
   }
   ```

## Request Testing

1. **GET Request Test**
   ```php
   class PostsControllerTest extends ControllerTestCase {
       public function testView() {
           $result = $this->testAction('/posts/view/1');
           $this->assertContains('Post Title', $result);
       }
   }
   ```

2. **POST Request Test**
   ```php
   class PostsControllerTest extends ControllerTestCase {
       public function testAdd() {
           $data = array(
               'Post' => array(
                   'title' => 'New Post',
                   'body' => 'Post content'
               )
           );
           $result = $this->testAction(
               '/posts/add',
               array('method' => 'post', 'data' => $data)
           );
           $this->assertContains('Post saved', $result);
       }
   }
   ```

## Component Testing

1. **Auth Component Test**
   ```php
   class PostsControllerTest extends ControllerTestCase {
       public function testAddRequiresAuth() {
           $this->testAction('/posts/add');
           $this->assertRedirect('/users/login');
       }
   }
   ```

2. **Session Component Test**
   ```php
   class PostsControllerTest extends ControllerTestCase {
       public function testFlashMessage() {
           $this->testAction('/posts/add');
           $this->assertSession('Post saved', 'Message.flash.message');
       }
   }
   ```

## Response Testing

1. **Response Status Test**
   ```php
   class PostsControllerTest extends ControllerTestCase {
       public function testNotFound() {
           $this->testAction('/posts/view/999');
           $this->assertResponseCode(404);
       }
   }
   ```

2. **Response Type Test**
   ```php
   class PostsControllerTest extends ControllerTestCase {
       public function testJsonResponse() {
           $this->testAction('/posts/api');
           $this->assertResponseType('json');
       }
   }
   ```

## Best Practices

1. **Test Design**
   - Test all actions
   - Test error cases
   - Test security
   - Test validation

2. **Test Organization**
   - Use fixtures
   - Group related tests
   - Document tests
   - Keep tests focused

3. **Test Coverage**
   - Test all paths
   - Test edge cases
   - Test security
   - Test validation

4. **Maintenance**
   - Update tests regularly
   - Review test coverage
   - Document changes
   - Keep tests simple 