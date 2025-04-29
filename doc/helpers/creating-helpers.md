# Creating Helpers

This guide covers creating custom helpers in CakePHP 2.x.

## Basic Helper

1. **Helper Creation**
   ```php
   // app/View/Helper/CustomHelper.php
   App::uses('AppHelper', 'View/Helper');
   
   class CustomHelper extends AppHelper {
       public $helpers = array('Html', 'Form');
       
       public function customMethod($param) {
           return $this->Html->tag('div', $param);
       }
   }
   ```

2. **Helper Usage**
   ```php
   // app/Controller/PostsController.php
   public $helpers = array('Custom');
   
   // app/View/Posts/index.ctp
   echo $this->Custom->customMethod('Content');
   ```

## Advanced Helper

1. **Helper with Settings**
   ```php
   // app/View/Helper/CustomHelper.php
   class CustomHelper extends AppHelper {
       public $settings = array(
           'option1' => 'default1',
           'option2' => 'default2'
       );
       
       public function __construct(View $View, $settings = array()) {
           parent::__construct($View, $settings);
           $this->settings = array_merge($this->settings, $settings);
       }
   }
   ```

2. **Helper Configuration**
   ```php
   // app/Controller/PostsController.php
   public $helpers = array(
       'Custom' => array(
           'option1' => 'value1',
           'option2' => 'value2'
       )
   );
   ```

## Helper Methods

1. **Basic Methods**
   ```php
   // app/View/Helper/CustomHelper.php
   public function formatDate($date) {
       return date('Y-m-d', strtotime($date));
   }
   
   public function formatCurrency($amount) {
       return '$' . number_format($amount, 2);
   }
   ```

2. **Advanced Methods**
   ```php
   // app/View/Helper/CustomHelper.php
   public function generateMenu($items) {
       $output = '<ul>';
       foreach ($items as $item) {
           $output .= $this->Html->tag('li', 
               $this->Html->link($item['title'], $item['url'])
           );
       }
       $output .= '</ul>';
       return $output;
   }
   ```

## Best Practices

1. **Helper Design**
   - Keep focused
   - Use inheritance
   - Document methods
   - Follow conventions

2. **Code Organization**
   - Group related methods
   - Use meaningful names
   - Maintain consistency
   - Version control

3. **Performance**
   - Optimize methods
   - Cache results
   - Minimize processing
   - Regular review

4. **Maintenance**
   - Update documentation
   - Test thoroughly
   - Handle errors
   - Regular updates 