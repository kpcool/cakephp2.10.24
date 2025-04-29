# Component Callbacks

This guide covers component callbacks in CakePHP 2.x.

## Lifecycle Callbacks

1. **Initialize Callback**
   ```php
   class ExampleComponent extends Component {
       public function initialize(Controller $controller) {
           // Called before controller's beforeFilter
           $this->controller = $controller;
       }
   }
   ```

2. **Startup Callback**
   ```php
   class ExampleComponent extends Component {
       public function startup(Controller $controller) {
           // Called after controller's beforeFilter
           $this->setup();
       }
   }
   ```

## Render Callbacks

1. **BeforeRender Callback**
   ```php
   class ExampleComponent extends Component {
       public function beforeRender(Controller $controller) {
           // Called before controller's render
           $controller->set('data', $this->data);
       }
   }
   ```

2. **Shutdown Callback**
   ```php
   class ExampleComponent extends Component {
       public function shutdown(Controller $controller) {
           // Called after controller's render
           $this->cleanup();
       }
   }
   ```

## Custom Callbacks

1. **Event-based Callbacks**
   ```php
   class ExampleComponent extends Component {
       public function implementedEvents() {
           return array(
               'Controller.beforeFilter' => 'beforeFilter',
               'Controller.afterFilter' => 'afterFilter'
           );
       }
       
       public function beforeFilter($event) {
           // Handle beforeFilter event
       }
   }
   ```

2. **Method-based Callbacks**
   ```php
   class ExampleComponent extends Component {
       public function beforeAction($controller, $settings) {
           // Called before controller action
       }
       
       public function afterAction($controller, $settings) {
           // Called after controller action
       }
   }
   ```

## Callback Usage

1. **Controller Integration**
   ```php
   class ExampleController extends AppController {
       public $components = array('Example');
       
       public function beforeFilter() {
           parent::beforeFilter();
           // Controller beforeFilter
       }
   }
   ```

2. **View Integration**
   ```php
   // In view
   $this->Example->beforeRender($this);
   ```

## Best Practices

1. **Callback Design**
   - Use meaningful names
   - Document callbacks
   - Handle errors
   - Test thoroughly

2. **Performance**
   - Optimize callbacks
   - Cache data
   - Monitor usage
   - Regular review

3. **Security**
   - Validate data
   - Sanitize input
   - Handle errors
   - Regular audits

4. **Maintenance**
   - Document changes
   - Version callbacks
   - Monitor usage
   - Regular updates 