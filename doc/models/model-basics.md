# Model Basics

This guide covers the fundamental concepts of Models in CakePHP 2.x.

## Creating Models

1. **Basic Model Structure**
   ```php
   class Post extends AppModel {
       public $name = 'Post';
       public $useTable = 'posts';
       public $primaryKey = 'id';
       public $displayField = 'title';
   }
   ```

2. **Model Properties**
   - `$name`: Model name
   - `$useTable`: Database table name
   - `$primaryKey`: Primary key field
   - `$displayField`: Field used for display purposes
   - `$useDbConfig`: Database configuration to use

## Basic Operations

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
       array('title' => 'First Post'),
       array('title' => 'Second Post')
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

## Model Configuration

1. **Table Configuration**
   ```php
   class Post extends AppModel {
       public $useTable = 'blog_posts';
       public $tablePrefix = 'app_';
   }
   ```

2. **Database Configuration**
   ```php
   class Post extends AppModel {
       public $useDbConfig = 'alternate';
   }
   ```

3. **Cache Configuration**
   ```php
   class Post extends AppModel {
       public $cacheQueries = true;
       public $cacheSources = true;
   }
   ```

## Best Practices

1. **Naming Conventions**
   - Use singular model names
   - Use plural table names
   - Follow CakePHP naming conventions

2. **Code Organization**
   - Keep models focused
   - Use behaviors for reusable code
   - Implement proper validation

3. **Performance**
   - Use proper indexing
   - Implement caching
   - Optimize queries

4. **Security**
   - Validate all input
   - Sanitize data
   - Use proper access control 