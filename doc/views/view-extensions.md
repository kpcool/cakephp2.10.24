# View Extensions

This guide covers view extensions in CakePHP 2.x.

## Basic Extensions

1. **View Extension**
   ```php
   // app/View/Posts/index.ctp
   <?php $this->extend('parent_view'); ?>
   <?php $this->start('content'); ?>
   <div class="content">
       <?php echo $content_for_layout; ?>
   </div>
   <?php $this->end(); ?>
   ```

2. **Parent View**
   ```php
   // app/View/Posts/parent_view.ctp
   <div class="container">
       <?php echo $this->fetch('content'); ?>
   </div>
   ```

## Extension Features

1. **Multiple Extensions**
   ```php
   // app/View/Posts/index.ctp
   <?php $this->extend('parent_view'); ?>
   <?php $this->start('sidebar'); ?>
   <div class="sidebar">
       <?php echo $this->element('sidebar'); ?>
   </div>
   <?php $this->end(); ?>
   ```

2. **Extension Variables**
   ```php
   // app/View/Posts/index.ctp
   <?php $this->extend('parent_view', array('class' => 'custom')); ?>
   <div class="content <?php echo $class; ?>">
       <?php echo $content_for_layout; ?>
   </div>
   ```

## Advanced Extensions

1. **Plugin Extensions**
   ```php
   // app/View/Posts/index.ctp
   <?php $this->extend('Plugin.parent_view'); ?>
   <?php $this->start('content'); ?>
   <div class="content">
       <?php echo $content_for_layout; ?>
   </div>
   <?php $this->end(); ?>
   ```

2. **Theme Extensions**
   ```php
   // app/View/Posts/index.ctp
   <?php $this->extend('Theme.parent_view'); ?>
   <?php $this->start('content'); ?>
   <div class="content">
       <?php echo $content_for_layout; ?>
   </div>
   <?php $this->end(); ?>
   ```

## Best Practices

1. **Extension Design**
   - Keep extensions focused
   - Use meaningful names
   - Follow conventions
   - Document usage

2. **Code Organization**
   - Group related extensions
   - Maintain consistency
   - Use inheritance
   - Version control

3. **Performance**
   - Minimize nesting
   - Cache extensions
   - Optimize content
   - Regular review

4. **Maintenance**
   - Update documentation
   - Test extensions
   - Handle errors
   - Regular updates 