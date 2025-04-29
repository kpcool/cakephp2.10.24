# Plugin Events

This guide covers plugin events in CakePHP 2.x.

## Event System

1. **Event Manager**
   ```php
   // In controller
   $eventManager = CakeEventManager::instance();
   ```

2. **Event Dispatching**
   ```php
   // In controller
   $event = new CakeEvent('PluginName.eventName', $this, array(
       'data' => $data
   ));
   $this->getEventManager()->dispatch($event);
   ```

## Event Listeners

1. **Attaching Listeners**
   ```php
   // In bootstrap
   CakeEventManager::instance()->attach(
       function($event) {
           // Handle event
       },
       'PluginName.eventName'
   );
   ```

2. **Class Listeners**
   ```php
   // In plugin class
   class PluginNameListener {
       public function implementedEvents() {
           return array(
               'PluginName.eventName' => 'handleEvent'
           );
       }
       
       public function handleEvent($event) {
           // Handle event
       }
   }
   ```

## Event Types

1. **Controller Events**
   ```php
   // In controller
   public function beforeFilter() {
       $event = new CakeEvent('Controller.beforeFilter', $this);
       $this->getEventManager()->dispatch($event);
   }
   ```

2. **Model Events**
   ```php
   // In model
   public function beforeSave($options = array()) {
       $event = new CakeEvent('Model.beforeSave', $this, array(
           'options' => $options
       ));
       $this->getEventManager()->dispatch($event);
   }
   ```

## Event Data

1. **Event Subject**
   ```php
   // In listener
   public function handleEvent($event) {
       $subject = $event->subject();
       $data = $event->data;
   }
   ```

2. **Event Results**
   ```php
   // In listener
   public function handleEvent($event) {
       $event->result = array(
           'success' => true,
           'data' => $data
       );
   }
   ```

## Best Practices

1. **Event Design**
   - Use meaningful names
   - Document events
   - Handle errors
   - Test thoroughly

2. **Performance**
   - Optimize listeners
   - Cache data
   - Monitor usage
   - Regular review

3. **Security**
   - Validate data
   - Sanitize input
   - Handle errors
   - Regular audits

4. **Maintenance**
   - Document changes
   - Version events
   - Monitor usage
   - Regular updates 