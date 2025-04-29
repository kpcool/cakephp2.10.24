# Helper Basics

This guide covers the fundamentals of using Helpers in CakePHP 2.x.

## Loading Helpers

1. **Controller Loading**
   ```php
   // app/Controller/PostsController.php
   public $helpers = array('Html', 'Form', 'Session');
   ```

2. **Dynamic Loading**
   ```php
   // app/Controller/PostsController.php
   public function beforeRender() {
       $this->helpers[] = 'Custom';
   }
   ```

## Basic Usage

1. **View Usage**
   ```php
   // app/View/Posts/index.ctp
   echo $this->Html->link('Home', '/');
   echo $this->Form->create('Post');
   echo $this->Session->flash();
   ```

2. **Helper Methods**
   ```php
   // app/View/Posts/index.ctp
   echo $this->Html->tag('div', 'Content', array('class' => 'container'));
   echo $this->Form->input('title');
   echo $this->Session->setFlash('Message');
   ```

## Helper Properties

1. **Common Properties**
   ```php
   // In helpers
   public $helpers = array('Html', 'Form');
   public $settings = array();
   public $view = null;
   ```

2. **Property Usage**
   ```php
   // In helpers
   public function initialize($settings = array()) {
       $this->settings = array_merge($this->settings, $settings);
   }
   ```

## Best Practices

1. **Helper Usage**
   - Load only needed helpers
   - Use appropriate helpers
   - Follow conventions
   - Document usage

2. **Performance**
   - Minimize helper loading
   - Cache helper output
   - Optimize methods
   - Regular review

3. **Maintenance**
   - Keep helpers focused
   - Update documentation
   - Test functionality
   - Version control

4. **Security**
   - Validate input
   - Escape output
   - Handle errors
   - Regular security review 