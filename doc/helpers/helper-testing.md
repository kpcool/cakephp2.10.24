# Helper Testing

This guide covers testing helpers in CakePHP 2.x.

## Basic Testing

1. **Test Setup**
   ```php
   // app/Test/Case/View/Helper/CustomHelperTest.php
   App::uses('CustomHelper', 'View/Helper');
   App::uses('View', 'View');
   App::uses('Controller', 'Controller');
   
   class CustomHelperTest extends CakeTestCase {
       public function setUp() {
           parent::setUp();
           $View = new View();
           $this->Custom = new CustomHelper($View);
       }
   }
   ```

2. **Basic Tests**
   ```php
   // app/Test/Case/View/Helper/CustomHelperTest.php
   public function testCustomMethod() {
       $result = $this->Custom->customMethod('test');
       $expected = '<div>test</div>';
       $this->assertEquals($expected, $result);
   }
   ```

## Advanced Testing

1. **Mock Objects**
   ```php
   // app/Test/Case/View/Helper/CustomHelperTest.php
   public function testHelperWithMock() {
       $View = $this->getMock('View', array('element'));
       $View->expects($this->once())
           ->method('element')
           ->with('custom_element');
           
       $Custom = new CustomHelper($View);
       $Custom->renderElement();
   }
   ```

2. **Helper Dependencies**
   ```php
   // app/Test/Case/View/Helper/CustomHelperTest.php
   public function testHelperDependencies() {
       $View = new View();
       $this->Custom->Html = $this->getMock('HtmlHelper', array('link'), array($View));
       $this->Custom->Html->expects($this->once())
           ->method('link')
           ->with('Home', '/');
           
       $this->Custom->generateLink('Home', '/');
   }
   ```

## Test Cases

1. **Input Validation**
   ```php
   // app/Test/Case/View/Helper/CustomHelperTest.php
   public function testInputValidation() {
       $result = $this->Custom->formatInput(null);
       $this->assertEmpty($result);
       
       $result = $this->Custom->formatInput('test');
       $this->assertEquals('TEST', $result);
   }
   ```

2. **Output Testing**
   ```php
   // app/Test/Case/View/Helper/CustomHelperTest.php
   public function testOutputFormatting() {
       $result = $this->Custom->formatOutput(array('test'));
       $this->assertContains('test', $result);
       $this->assertNotContains('invalid', $result);
   }
   ```

## Best Practices

1. **Test Design**
   - Test all methods
   - Use meaningful names
   - Document tests
   - Follow conventions

2. **Test Organization**
   - Group related tests
   - Maintain consistency
   - Use inheritance
   - Version control

3. **Test Coverage**
   - Test edge cases
   - Test error conditions
   - Test all paths
   - Regular review

4. **Maintenance**
   - Update tests
   - Document changes
   - Handle failures
   - Regular updates 