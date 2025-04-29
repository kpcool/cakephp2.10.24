# Plugin Testing

This guide covers testing plugins in CakePHP 2.x.

## Test Setup

1. **Test Directory**
   ```
   Plugin/PluginName/Test/
   ├── Case/
   │   ├── Controller/
   │   ├── Model/
   │   └── View/
   └── bootstrap.php
   ```

2. **Test Bootstrap**
   ```php
   // Plugin/PluginName/Test/bootstrap.php
   App::uses('CakeTestCase', 'TestSuite');
   App::uses('ControllerTestCase', 'TestSuite');
   ```

## Controller Tests

1. **Basic Test**
   ```php
   // Plugin/PluginName/Test/Case/Controller/PluginNameControllerTest.php
   class PluginNameControllerTest extends ControllerTestCase {
       public function testIndex() {
           $result = $this->testAction('/plugin_name/index');
           $this->assertContains('expected', $result);
       }
   }
   ```

2. **Mock Objects**
   ```php
   // In test
   $this->controller = $this->generate('PluginName.PluginName', array(
       'components' => array('Session'),
       'models' => array('PluginName.PluginName')
   ));
   ```

## Model Tests

1. **Basic Test**
   ```php
   // Plugin/PluginName/Test/Case/Model/PluginNameTest.php
   class PluginNameTest extends CakeTestCase {
       public function testFind() {
           $result = $this->PluginName->find('all');
           $this->assertNotEmpty($result);
       }
   }
   ```

2. **Data Fixtures**
   ```php
   // Plugin/PluginName/Test/Fixture/PluginNameFixture.php
   class PluginNameFixture extends CakeTestFixture {
       public $import = array('model' => 'PluginName.PluginName');
   }
   ```

## View Tests

1. **Basic Test**
   ```php
   // Plugin/PluginName/Test/Case/View/PluginNameViewTest.php
   class PluginNameViewTest extends CakeTestCase {
       public function testRender() {
           $View = new View();
           $result = $View->element('PluginName.element_name');
           $this->assertContains('expected', $result);
       }
   }
   ```

2. **Helper Tests**
   ```php
   // Plugin/PluginName/Test/Case/View/Helper/PluginNameHelperTest.php
   class PluginNameHelperTest extends CakeTestCase {
       public function testMethod() {
           $View = new View();
           $Helper = new PluginNameHelper($View);
           $result = $Helper->method();
           $this->assertEquals('expected', $result);
       }
   }
   ```

## Best Practices

1. **Test Design**
   - Test all features
   - Use meaningful names
   - Document tests
   - Handle errors

2. **Code Coverage**
   - Aim for high coverage
   - Test edge cases
   - Regular review
   - Update tests

3. **Performance**
   - Optimize tests
   - Use fixtures
   - Cache data
   - Regular cleanup

4. **Maintenance**
   - Update documentation
   - Version tests
   - Monitor results
   - Regular updates 