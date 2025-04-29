# Built-in Helpers

This guide covers the built-in helpers available in CakePHP 2.x.

## HTML Helper

1. **Basic HTML**
   ```php
   // In views
   echo $this->Html->link('Home', '/');
   echo $this->Html->image('logo.png');
   echo $this->Html->tag('div', 'Content');
   ```

2. **Advanced HTML**
   ```php
   // In views
   echo $this->Html->script('app.js');
   echo $this->Html->css('style.css');
   echo $this->Html->meta('description', 'Site description');
   ```

## Form Helper

1. **Basic Forms**
   ```php
   // In views
   echo $this->Form->create('Post');
   echo $this->Form->input('title');
   echo $this->Form->input('body');
   echo $this->Form->end('Save');
   ```

2. **Advanced Forms**
   ```php
   // In views
   echo $this->Form->input('category_id', array('type' => 'select'));
   echo $this->Form->input('published', array('type' => 'checkbox'));
   echo $this->Form->input('created', array('type' => 'datetime'));
   ```

## Session Helper

1. **Session Management**
   ```php
   // In views
   echo $this->Session->flash();
   echo $this->Session->read('User.name');
   echo $this->Session->check('User.id');
   ```

2. **Flash Messages**
   ```php
   // In controllers
   $this->Session->setFlash('Message', 'default', array('class' => 'success'));
   $this->Session->setFlash('Error', 'default', array('class' => 'error'));
   ```

## Paginator Helper

1. **Basic Pagination**
   ```php
   // In views
   echo $this->Paginator->numbers();
   echo $this->Paginator->prev('« Previous');
   echo $this->Paginator->next('Next »');
   ```

2. **Advanced Pagination**
   ```php
   // In views
   echo $this->Paginator->counter(array(
       'format' => 'Page {:page} of {:pages}, showing {:current} records'
   ));
   echo $this->Paginator->sort('title');
   ```

## Text Helper

1. **Text Formatting**
   ```php
   // In views
   echo $this->Text->truncate($text, 100);
   echo $this->Text->excerpt($text, 'keyword', 50);
   echo $this->Text->highlight($text, 'keyword');
   ```

2. **String Operations**
   ```php
   // In views
   echo $this->Text->autoLink($text);
   echo $this->Text->autoParagraph($text);
   echo $this->Text->stripLinks($text);
   ```

## Best Practices

1. **Helper Usage**
   - Use appropriate helpers
   - Follow conventions
   - Document usage
   - Regular review

2. **Performance**
   - Minimize helper loading
   - Cache output
   - Optimize methods
   - Monitor usage

3. **Maintenance**
   - Keep updated
   - Test functionality
   - Document changes
   - Version control

4. **Security**
   - Validate input
   - Escape output
   - Handle errors
   - Regular security review 