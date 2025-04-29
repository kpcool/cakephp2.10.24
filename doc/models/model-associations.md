# Model Associations

This guide covers model associations in CakePHP 2.x.

## Association Types

1. **BelongsTo**
   ```php
   class Comment extends AppModel {
       public $belongsTo = array(
           'Post' => array(
               'className' => 'Post',
               'foreignKey' => 'post_id',
               'conditions' => array('Post.status' => 'published'),
               'fields' => array('id', 'title'),
               'order' => array('Post.created' => 'DESC')
           )
       );
   }
   ```

2. **HasMany**
   ```php
   class Post extends AppModel {
       public $hasMany = array(
           'Comment' => array(
               'className' => 'Comment',
               'foreignKey' => 'post_id',
               'dependent' => true,
               'conditions' => array('Comment.status' => 'approved'),
               'fields' => array('id', 'body', 'created'),
               'order' => array('Comment.created' => 'ASC'),
               'limit' => 5
           )
       );
   }
   ```

3. **HasAndBelongsToMany**
   ```php
   class Post extends AppModel {
       public $hasAndBelongsToMany = array(
           'Tag' => array(
               'className' => 'Tag',
               'joinTable' => 'posts_tags',
               'foreignKey' => 'post_id',
               'associationForeignKey' => 'tag_id',
               'unique' => true,
               'conditions' => array(),
               'fields' => array('id', 'name'),
               'order' => array('Tag.name' => 'ASC'),
               'limit' => 10
           )
       );
   }
   ```

## Association Options

1. **Common Options**
   - `className`: Associated model name
   - `foreignKey`: Foreign key field
   - `conditions`: Query conditions
   - `fields`: Fields to retrieve
   - `order`: Result ordering
   - `limit`: Result limit
   - `offset`: Result offset

2. **Special Options**
   - `dependent`: Delete associated records
   - `counterCache`: Cache counts
   - `unique`: Keep unique associations
   - `finderQuery`: Custom find query

## Working with Associations

1. **Saving Associated Data**
   ```php
   // Save with belongsTo
   $this->Comment->save(array(
       'Comment' => array('body' => 'New comment'),
       'Post' => array('id' => 1)
   ));
   
   // Save with hasMany
   $this->Post->save(array(
       'Post' => array('title' => 'New post'),
       'Comment' => array(
           array('body' => 'First comment'),
           array('body' => 'Second comment')
       )
   ));
   ```

2. **Finding with Associations**
   ```php
   // Find with belongsTo
   $comments = $this->Comment->find('all', array(
       'contain' => array('Post')
   ));
   
   // Find with hasMany
   $posts = $this->Post->find('all', array(
       'contain' => array('Comment')
   ));
   ```

3. **Deleting with Associations**
   ```php
   // Delete with dependent
   $this->Post->delete($id); // Will delete associated comments
   
   // Delete without dependent
   $this->Post->delete($id, false); // Won't delete associated comments
   ```

## Best Practices

1. **Association Design**
   - Use appropriate association types
   - Set proper foreign keys
   - Implement proper indexing
   - Use counterCache when needed

2. **Performance**
   - Use containable behavior
   - Limit associated data
   - Implement proper indexing
   - Cache when appropriate

3. **Data Integrity**
   - Use proper foreign keys
   - Implement cascading deletes
   - Validate associated data
   - Use transactions when needed

4. **Maintenance**
   - Document associations
   - Keep associations simple
   - Regular cleanup
   - Monitor performance 