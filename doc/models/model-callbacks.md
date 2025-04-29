# Model Callbacks

This guide covers model callbacks in CakePHP 2.x.

## Callback Types

1. **Before Callbacks**
   ```php
   class Post extends AppModel {
       public function beforeValidate($options = array()) {
           // Modify data before validation
           if (isset($this->data[$this->alias]['title'])) {
               $this->data[$this->alias]['slug'] = Inflector::slug($this->data[$this->alias]['title']);
           }
           return true;
       }
       
       public function beforeSave($options = array()) {
           // Modify data before save
           if (isset($this->data[$this->alias]['body'])) {
               $this->data[$this->alias]['body'] = strip_tags($this->data[$this->alias]['body']);
           }
           return true;
       }
       
       public function beforeDelete($cascade = true) {
           // Check before delete
           return true;
       }
   }
   ```

2. **After Callbacks**
   ```php
   class Post extends AppModel {
       public function afterValidate() {
           // Actions after validation
       }
       
       public function afterSave($created, $options = array()) {
           if ($created) {
               // Handle new record
           } else {
               // Handle updated record
           }
       }
       
       public function afterDelete() {
           // Cleanup after delete
       }
   }
   ```

## Common Callbacks

1. **Find Callbacks**
   ```php
   class Post extends AppModel {
       public function beforeFind($queryData) {
           // Modify query before find
           return $queryData;
       }
       
       public function afterFind($results, $primary = false) {
           // Modify results after find
           return $results;
       }
   }
   ```

2. **Save Callbacks**
   ```php
   class Post extends AppModel {
       public function beforeSave($options = array()) {
           // Before save logic
           return true;
       }
       
       public function afterSave($created, $options = array()) {
           // After save logic
       }
   }
   ```

## Working with Callbacks

1. **Callback Options**
   ```php
   class Post extends AppModel {
       public function beforeSave($options = array()) {
           // Access options
           $validate = $options['validate'];
           $fieldList = $options['fieldList'];
           return true;
       }
   }
   ```

2. **Callback Return Values**
   ```php
   class Post extends AppModel {
       public function beforeSave($options = array()) {
           // Return false to abort save
           if ($someCondition) {
               return false;
           }
           return true;
       }
   }
   ```

3. **Callback Data**
   ```php
   class Post extends AppModel {
       public function beforeSave($options = array()) {
           // Access model data
           $data = $this->data;
           $alias = $this->alias;
           return true;
       }
   }
   ```

## Best Practices

1. **Callback Design**
   - Keep callbacks focused
   - Document callback purpose
   - Consider performance
   - Handle errors properly

2. **Performance**
   - Minimize callback logic
   - Cache when appropriate
   - Optimize queries
   - Consider timing

3. **Maintenance**
   - Document callbacks
   - Keep callbacks simple
   - Regular review
   - Update as needed

4. **Security**
   - Validate data
   - Sanitize input
   - Check permissions
   - Handle errors 