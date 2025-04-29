# Models

This guide covers the Model layer in CakePHP 2.x, which handles data and business logic.

## Model Basics

1. **Creating Models**
   ```php
   class Post extends AppModel {
       public $name = 'Post';
       public $useTable = 'posts';
       public $primaryKey = 'id';
       public $displayField = 'title';
   }
   ```

2. **Model Associations**
   ```php
   class Post extends AppModel {
       public $belongsTo = array(
           'User' => array(
               'className' => 'User',
               'foreignKey' => 'user_id'
           )
       );
       
       public $hasMany = array(
           'Comment' => array(
               'className' => 'Comment',
               'foreignKey' => 'post_id',
               'dependent' => true
           )
       );
       
       public $hasAndBelongsToMany = array(
           'Tag' => array(
               'className' => 'Tag',
               'joinTable' => 'posts_tags',
               'foreignKey' => 'post_id',
               'associationForeignKey' => 'tag_id'
           )
       );
   }
   ```

3. **Validation Rules**
   ```php
   class Post extends AppModel {
       public $validate = array(
           'title' => array(
               'rule' => 'notEmpty',
               'message' => 'Title is required',
               'required' => true
           ),
           'body' => array(
               'rule' => array('minLength', 10),
               'message' => 'Body must be at least 10 characters long'
           ),
           'email' => array(
               'rule' => 'email',
               'message' => 'Please enter a valid email address'
           )
       );
   }
   ```

## Data Operations

1. **Creating Records**
   ```php
   // Single record
   $this->Post->create();
   $this->Post->save(array(
       'title' => 'New Post',
       'body' => 'Post content'
   ));
   
   // Multiple records
   $this->Post->saveMany(array(
       array('title' => 'First Post', 'body' => 'Content 1'),
       array('title' => 'Second Post', 'body' => 'Content 2')
   ));
   ```

2. **Reading Records**
   ```php
   // Find all records
   $posts = $this->Post->find('all');
   
   // Find by ID
   $post = $this->Post->findById($id);
   
   // Find with conditions
   $posts = $this->Post->find('all', array(
       'conditions' => array('Post.status' => 'published'),
       'order' => array('Post.created' => 'DESC'),
       'limit' => 10
   ));
   
   // Find first matching record
   $post = $this->Post->find('first', array(
       'conditions' => array('Post.slug' => $slug)
   ));
   ```

3. **Updating Records**
   ```php
   // Update by ID
   $this->Post->id = $id;
   $this->Post->save(array('title' => 'Updated Title'));
   
   // Update with conditions
   $this->Post->updateAll(
       array('Post.status' => "'published'"),
       array('Post.created <' => date('Y-m-d'))
   );
   ```

4. **Deleting Records**
   ```php
   // Delete by ID
   $this->Post->delete($id);
   
   // Delete with conditions
   $this->Post->deleteAll(array('Post.status' => 'draft'));
   ```

## Model Behaviors

1. **Using Behaviors**
   ```php
   class Post extends AppModel {
       public $actsAs = array(
           'Containable',
           'Sluggable' => array(
               'label' => 'title',
               'slug' => 'slug',
               'separator' => '-'
           ),
           'Tree' => array(
               'parent' => 'parent_id',
               'left' => 'lft',
               'right' => 'rght'
           )
       );
   }
   ```

2. **Common Behaviors**
   - Containable: Control associated data loading
   - Sluggable: Generate URL-friendly slugs
   - Tree: Handle hierarchical data
   - SoftDelete: Soft delete records
   - Timestamp: Auto-update timestamps
   - Searchable: Advanced search functionality
   - Upload: File upload handling

## Callbacks

1. **Before Callbacks**
   ```php
   class Post extends AppModel {
       public function beforeSave($options = array()) {
           if (isset($this->data[$this->alias]['title'])) {
               $this->data[$this->alias]['slug'] = Inflector::slug($this->data[$this->alias]['title']);
           }
           return true;
       }
       
       public function beforeValidate($options = array()) {
           // Modify data before validation
           return true;
       }
   }
   ```

2. **After Callbacks**
   ```php
   class Post extends AppModel {
       public function afterSave($created, $options = array()) {
           if ($created) {
               // Handle new record
           } else {
               // Handle updated record
           }
       }
       
       public function afterFind($results, $primary = false) {
           // Modify results after find
           return $results;
       }
   }
   ```

## Data Validation

1. **Validation Rules**
   ```php
   class Post extends AppModel {
       public $validate = array(
           'title' => array(
               'rule' => array('minLength', 5),
               'message' => 'Title must be at least 5 characters',
               'allowEmpty' => false
           ),
           'email' => array(
               'rule' => 'email',
               'message' => 'Please enter a valid email'
           ),
           'status' => array(
               'rule' => array('inList', array('draft', 'published', 'archived')),
               'message' => 'Please enter a valid status'
           )
       );
   }
   ```

2. **Custom Validation Rules**
   ```php
   class Post extends AppModel {
       public $validate = array(
           'title' => array(
               'rule' => array('customValidation'),
               'message' => 'Custom validation failed'
           )
       );
       
       public function customValidation($check) {
           // Custom validation logic
           return strpos($check, 'test') === false;
       }
   }
   ```

## Best Practices

1. **Data Access**
   - Use proper indexing
   - Limit returned fields
   - Use containable for associations
   - Implement query caching
   - Use transactions for multiple operations

2. **Validation**
   - Validate all input
   - Use appropriate rules
   - Implement custom validation when needed
   - Use client-side validation
   - Sanitize data before saving

3. **Performance**
   - Optimize database queries
   - Use proper indexing
   - Implement caching
   - Use containable for associations
   - Limit returned data

4. **Security**
   - Validate all input
   - Sanitize output
   - Use prepared statements
   - Implement proper access control
   - Use CSRF protection 