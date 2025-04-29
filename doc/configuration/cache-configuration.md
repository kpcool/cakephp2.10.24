# Cache Configuration

This guide covers cache configuration in CakePHP 2.x.

## Cache Settings

1. **Basic Configuration**
   ```php
   // app/Config/core.php
   Cache::config('default', array(
       'engine' => 'File',
       'duration' => '+1 hour',
       'path' => CACHE,
       'prefix' => 'cake_',
       'lock' => false
   ));
   ```

2. **Multiple Cache Configs**
   ```php
   // app/Config/core.php
   Cache::config('short', array(
       'engine' => 'File',
       'duration' => '+1 hour',
       'path' => CACHE . 'short' . DS,
       'prefix' => 'cake_short_'
   ));
   
   Cache::config('long', array(
       'engine' => 'File',
       'duration' => '+1 week',
       'path' => CACHE . 'long' . DS,
       'prefix' => 'cake_long_'
   ));
   ```

## Cache Engines

1. **File Cache**
   ```php
   // app/Config/core.php
   Cache::config('default', array(
       'engine' => 'File',
       'duration' => '+1 hour',
       'path' => CACHE,
       'prefix' => 'cake_',
       'lock' => false
   ));
   ```

2. **APC Cache**
   ```php
   // app/Config/core.php
   Cache::config('default', array(
       'engine' => 'Apc',
       'duration' => '+1 hour',
       'prefix' => 'cake_'
   ));
   ```

3. **Memcached Cache**
   ```php
   // app/Config/core.php
   Cache::config('default', array(
       'engine' => 'Memcached',
       'duration' => '+1 hour',
       'prefix' => 'cake_',
       'servers' => array(
           '127.0.0.1:11211'
       )
   ));
   ```

## Cache Usage

1. **Writing to Cache**
   ```php
   // In your controller or model
   Cache::write('key', $value, 'default');
   Cache::write('key', $value, 'short');
   Cache::write('key', $value, 'long');
   ```

2. **Reading from Cache**
   ```php
   // In your controller or model
   $value = Cache::read('key', 'default');
   $value = Cache::read('key', 'short');
   $value = Cache::read('key', 'long');
   ```

## Best Practices

1. **Cache Design**
   - Choose appropriate engine
   - Set proper duration
   - Use meaningful keys
   - Consider cache size

2. **Performance**
   - Monitor cache hits
   - Optimize cache duration
   - Use appropriate engine
   - Regular maintenance

3. **Security**
   - Secure cache storage
   - Validate cache data
   - Monitor cache usage
   - Regular security review

4. **Maintenance**
   - Regular cache cleanup
   - Monitor cache size
   - Update configurations
   - Document changes 