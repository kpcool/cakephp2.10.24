# Behaviors

This guide covers model behaviors in CakePHP 2.x.

## Using Behaviors

1. **Basic Usage**
   ```php
   class Post extends AppModel {
       public $actsAs = array(
           'Containable',
           'Sluggable' => array(
               'label' => 'title',
               'slug' => 'slug',
               'separator' => '-'
           )
       );
   }
   ```

2. **Common Behaviors**
   ```php
   class Post extends AppModel {
       public $actsAs = array(
           'Containable',
           'Sluggable',
           'Tree' => array(
               'parent' => 'parent_id',
               'left' => 'lft',
               'right' => 'rght'
           ),
           'SoftDelete',
           'Timestamp'
       );
   }
   ```

## Creating Behaviors

1. **Basic Behavior**
   ```php
   class ExampleBehavior extends ModelBehavior {
       public function setup(Model $Model, $settings = array()) {
           // Setup behavior
       }
       
       public function cleanup(Model $Model) {
           // Cleanup behavior
       }
       
       public function beforeFind(Model $Model, $query) {
           // Modify query
           return $query;
       }
       
       public function afterFind(Model $Model, $results, $primary = false) {
           // Modify results
           return $results;
       }
   }
   ```

2. **Behavior Methods**
   ```php
   class ExampleBehavior extends ModelBehavior {
       public function customMethod(Model $Model, $param1, $param2) {
           // Custom behavior method
           return $result;
       }
   }
   ```

## Common Behaviors

1. **Containable**
   ```php
   class Post extends AppModel {
       public $actsAs = array('Containable');
       
       public function findWithComments() {
           return $this->find('all', array(
               'contain' => array('Comment')
           ));
       }
   }
   ```

2. **Sluggable**
   ```php
   class Post extends AppModel {
       public $actsAs = array(
           'Sluggable' => array(
               'label' => 'title',
               'slug' => 'slug',
               'separator' => '-',
               'overwrite' => false
           )
       );
   }
   ```

3. **Tree**
   ```php
   class Category extends AppModel {
       public $actsAs = array(
           'Tree' => array(
               'parent' => 'parent_id',
               'left' => 'lft',
               'right' => 'rght'
           )
       );
   }
   ```

## Working with Behaviors

1. **Loading Behaviors**
   ```php
   // Load in model
   public $actsAs = array('BehaviorName');
   
   // Load dynamically
   $this->Behaviors->load('BehaviorName');
   ```

2. **Unloading Behaviors**
   ```php
   // Unload behavior
   $this->Behaviors->unload('BehaviorName');
   ```

3. **Checking Behaviors**
   ```php
   // Check if behavior is loaded
   if ($this->Behaviors->enabled('BehaviorName')) {
       // Behavior is loaded
   }
   ```

## Best Practices

1. **Behavior Design**
   - Keep behaviors focused
   - Document behavior purpose
   - Consider performance
   - Handle errors properly

2. **Performance**
   - Minimize behavior logic
   - Cache when appropriate
   - Optimize queries
   - Consider timing

3. **Maintenance**
   - Document behaviors
   - Keep behaviors simple
   - Regular review
   - Update as needed

4. **Security**
   - Validate data
   - Sanitize input
   - Check permissions
   - Handle errors 