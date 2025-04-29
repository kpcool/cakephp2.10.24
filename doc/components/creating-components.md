# Creating Components

This guide covers how to create custom components in CakePHP 2.x.

## Component Creation

1. **Basic Component**
   ```php
   // app/Controller/Component/CustomComponent.php
   class CustomComponent extends Component {
       public function initialize(Controller $controller) {
           $this->controller = $controller;
       }
       
       public function customMethod() {
           // Custom logic
       }
   }
   ```

2. **Component with Settings**
   ```php
   // In controller
   public $components = array(
       'Custom' => array(
           'setting1' => 'value1',
           'setting2' => 'value2'
       )
   );
   
   // In component
   class CustomComponent extends Component {
       public function initialize(Controller $controller) {
           $this->settings = array_merge($this->settings, $this->settings);
       }
   }
   ```

## Component Methods

1. **Public Methods**
   ```php
   class CustomComponent extends Component {
       public function publicMethod($param) {
           // Public logic
           return $result;
       }
   }
   ```

2. **Protected Methods**
   ```php
   class CustomComponent extends Component {
       protected function _protectedMethod() {
           // Protected logic
       }
   }
   ```

## Component Properties

1. **Public Properties**
   ```php
   class CustomComponent extends Component {
       public $publicProperty;
       
       public function method() {
           $this->publicProperty = 'value';
       }
   }
   ```

2. **Protected Properties**
   ```php
   class CustomComponent extends Component {
       protected $_protectedProperty;
       
       protected function _method() {
           $this->_protectedProperty = 'value';
       }
   }
   ```

## Component Usage

1. **Controller Integration**
   ```php
   class ExampleController extends AppController {
       public $components = array('Custom');
       
       public function index() {
           $result = $this->Custom->customMethod();
       }
   }
   ```

2. **View Integration**
   ```php
   // In view
   $this->Custom->method();
   ```

## Best Practices

1. **Component Design**
   - Single responsibility
   - Clear interfaces
   - Document methods
   - Handle errors

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