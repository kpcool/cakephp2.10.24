# Helper Methods

This guide covers helper methods in CakePHP 2.x.

## Basic Methods

1. **HTML Methods**
   ```php
   // In views
   echo $this->Html->link('Home', '/');
   echo $this->Html->image('logo.png');
   echo $this->Html->tag('div', 'Content');
   ```

2. **Form Methods**
   ```php
   // In views
   echo $this->Form->create('Post');
   echo $this->Form->input('title');
   echo $this->Form->end('Save');
   ```

## Advanced Methods

1. **Custom Methods**
   ```php
   // app/View/Helper/CustomHelper.php
   public function formatDate($date) {
       return date('Y-m-d', strtotime($date));
   }
   
   public function generateMenu($items) {
       $output = '<ul>';
       foreach ($items as $item) {
           $output .= $this->Html->tag('li', 
               $this->Html->link($item['title'], $item['url'])
           );
       }
       return $output . '</ul>';
   }
   ```

2. **Helper Chaining**
   ```php
   // In views
   echo $this->Html->tag('div', 
       $this->Form->input('title') . 
       $this->Form->input('body')
   );
   ```

## Method Parameters

1. **Basic Parameters**
   ```php
   // In helpers
   public function customMethod($param1, $param2 = 'default') {
       return $param1 . $param2;
   }
   ```

2. **Array Parameters**
   ```php
   // In helpers
   public function customMethod($options = array()) {
       $defaults = array(
           'option1' => 'default1',
           'option2' => 'default2'
       );
       $options = array_merge($defaults, $options);
       return $options['option1'] . $options['option2'];
   }
   ```

## Best Practices

1. **Method Design**
   - Keep focused
   - Use meaningful names
   - Document parameters
   - Follow conventions

2. **Code Organization**
   - Group related methods
   - Maintain consistency
   - Use inheritance
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