# Component Basics

This guide covers the fundamentals of components in CakePHP 2.x.

## Basic Structure

1. **Component Class**
   ```php
   // app/Controller/Component/ExampleComponent.php
   class ExampleComponent extends Component {
       public function initialize(Controller $controller) {
           // Initialization code
       }
       
       public function startup(Controller $controller) {
           // Startup code
       }
   }
   ```

2. **Component Usage**
   ```php
   // app/Controller/ExampleController.php
   class ExampleController extends AppController {
       public $components = array('Example');
       
       public function index() {
           $this->Example->method();
       }
   }
   ```

## Component Methods

1. **Lifecycle Methods**
   ```php
   class ExampleComponent extends Component {
       public function initialize(Controller $controller) {
           // Called before controller's beforeFilter
       }
       
       public function startup(Controller $controller) {
           // Called after controller's beforeFilter
       }
       
       public function beforeRender(Controller $controller) {
           // Called before controller's render
       }
       
       public function shutdown(Controller $controller) {
           // Called after controller's render
       }
   }
   ```

2. **Custom Methods**
   ```php
   class ExampleComponent extends Component {
       public function customMethod($param) {
           // Custom logic
           return $result;
       }
   }
   ```

## Component Properties

1. **Controller Access**
   ```php
   class ExampleComponent extends Component {
       public function method() {
           $this->controller->method();
           $this->controller->property;
       }
   }
   ```

2. **Component Settings**
   ```php
   // In controller
   public $components = array(
       'Example' => array(
           'setting1' => 'value1',
           'setting2' => 'value2'
       )
   );
   ```

## Best Practices

1. **Component Design**
   - Single responsibility
   - Reusable logic
   - Clear interfaces
   - Document methods

2. **Code Organization**
   - Meaningful names
   - Proper namespacing
   - Consistent structure
   - Version control

3. **Performance**
   - Optimize methods
   - Cache data
   - Minimize dependencies
   - Regular review

4. **Maintenance**
   - Update documentation
   - Handle errors
   - Regular updates
   - Version tracking 