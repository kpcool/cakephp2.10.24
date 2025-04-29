# Layouts

This guide covers layouts in CakePHP 2.x.

## Basic Layout

1. **Default Layout**
   ```php
   // app/View/Layouts/default.ctp
   <!DOCTYPE html>
   <html>
   <head>
       <title><?php echo $title_for_layout; ?></title>
       <?php echo $this->Html->css('style'); ?>
       <?php echo $this->Html->script('app'); ?>
   </head>
   <body>
       <div id="header">
           <?php echo $this->element('header'); ?>
       </div>
       <div id="content">
           <?php echo $this->fetch('content'); ?>
       </div>
       <div id="footer">
           <?php echo $this->element('footer'); ?>
       </div>
   </body>
   </html>
   ```

2. **Layout Selection**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->layout = 'custom';
   }
   ```

## Layout Features

1. **Content Blocks**
   ```php
   // In views
   <?php $this->start('sidebar'); ?>
   <div class="sidebar">
       <?php echo $this->element('sidebar'); ?>
   </div>
   <?php $this->end(); ?>
   ```

2. **Layout Variables**
   ```php
   // app/Controller/AppController.php
   public function beforeRender() {
       $this->set('title_for_layout', 'My Site');
   }
   ```

## Custom Layouts

1. **Theme Layouts**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->theme = 'CustomTheme';
       $this->layout = 'custom';
   }
   ```

2. **Plugin Layouts**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $this->layout = 'Plugin.custom';
   }
   ```

## Best Practices

1. **Layout Design**
   - Keep layouts clean
   - Use semantic HTML
   - Follow conventions
   - Document structure

2. **Code Organization**
   - Separate concerns
   - Use elements
   - Maintain consistency
   - Version control

3. **Performance**
   - Minimize includes
   - Cache content
   - Optimize assets
   - Regular review

4. **Maintenance**
   - Update documentation
   - Test layouts
   - Handle errors
   - Regular updates 