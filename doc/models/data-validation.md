# Data Validation

This guide covers data validation in CakePHP 2.x.

## Validation Rules

1. **Basic Validation**
   ```php
   class Post extends AppModel {
       public $validate = array(
           'title' => array(
               'rule' => 'notEmpty',
               'message' => 'Title is required',
               'required' => true,
               'allowEmpty' => false
           ),
           'body' => array(
               'rule' => array('minLength', 10),
               'message' => 'Body must be at least 10 characters'
           ),
           'email' => array(
               'rule' => 'email',
               'message' => 'Please enter a valid email'
           )
       );
   }
   ```

2. **Multiple Rules**
   ```php
   class Post extends AppModel {
       public $validate = array(
           'title' => array(
               'notEmpty' => array(
                   'rule' => 'notEmpty',
                   'message' => 'Title is required'
               ),
               'minLength' => array(
                   'rule' => array('minLength', 5),
                   'message' => 'Title must be at least 5 characters'
               )
           )
       );
   }
   ```

## Validation Methods

1. **Built-in Rules**
   - `notEmpty`: Check if not empty
   - `email`: Validate email format
   - `url`: Validate URL format
   - `numeric`: Check if numeric
   - `minLength`: Minimum length
   - `maxLength`: Maximum length
   - `inList`: Value in list
   - `range`: Value in range
   - `date`: Valid date
   - `time`: Valid time
   - `datetime`: Valid datetime

2. **Custom Rules**
   ```php
   class Post extends AppModel {
       public $validate = array(
           'title' => array(
               'rule' => array('customValidation'),
               'message' => 'Custom validation failed'
           )
       );
       
       public function customValidation($check) {
           return strpos($check, 'test') === false;
       }
   }
   ```

## Validation Options

1. **Common Options**
   - `rule`: Validation rule
   - `message`: Error message
   - `required`: Field is required
   - `allowEmpty`: Allow empty values
   - `on`: When to validate (create/update)

2. **Advanced Options**
   - `last`: Stop validation if this rule fails
   - `allowEmpty`: Allow empty values
   - `required`: Field is required
   - `on`: When to validate

## Working with Validation

1. **Manual Validation**
   ```php
   $data = array('Post' => array('title' => 'New Post'));
   $this->Post->set($data);
   if ($this->Post->validates()) {
       // Data is valid
   } else {
       $errors = $this->Post->validationErrors;
   }
   ```

2. **Validation in Forms**
   ```php
   // In the view
   echo $this->Form->create('Post');
   echo $this->Form->input('title');
   echo $this->Form->input('body');
   echo $this->Form->end('Submit');
   ```

3. **Custom Error Messages**
   ```php
   class Post extends AppModel {
       public $validate = array(
           'title' => array(
               'rule' => 'notEmpty',
               'message' => 'Please enter a title for your post'
           )
       );
   }
   ```

## Best Practices

1. **Validation Design**
   - Validate all input
   - Use appropriate rules
   - Provide clear messages
   - Consider user experience

2. **Security**
   - Validate all input
   - Sanitize data
   - Use proper rules
   - Consider edge cases

3. **Performance**
   - Use efficient rules
   - Limit validation scope
   - Cache when appropriate
   - Optimize rules

4. **Maintenance**
   - Document rules
   - Keep rules simple
   - Regular review
   - Update as needed 