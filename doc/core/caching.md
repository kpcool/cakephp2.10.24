# Caching

This guide covers caching in CakePHP 2.x.

## Cache Configuration

1. **Basic Cache Setup**
   ```php
   // app/Config/core.php
   Cache::config('default', array(
       'engine' => 'File',
       'duration' => '+1 hour',
       'path' => CACHE,
       'prefix' => 'cake_'
   ));
   ```

2. **Multiple Cache Configs**
   ```php
   // app/Config/core.php
   Cache::config('short', array(
       'engine' => 'File',
       'duration' => '+5 minutes',
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
   Cache::config('file', array(
       'engine' => 'File',
       'duration' => '+1 hour',
       'path' => CACHE,
       'prefix' => 'cake_'
   ));
   ```

2. **APC Cache**
   ```php
   // app/Config/core.php
   Cache::config('apc', array(
       'engine' => 'Apc',
       'duration' => '+1 hour',
       'prefix' => 'cake_'
   ));
   ```

## Cache Usage

1. **Basic Caching**
   ```php
   // app/Controller/PostsController.php
   public function index() {
       $posts = Cache::read('posts_index');
       if (!$posts) {
           $posts = $this->Post->find('all');
           Cache::write('posts_index', $posts);
       }
       $this->set('posts', $posts);
   }
   ```

2. **Cache Groups**
   ```php
   // app/Controller/PostsController.php
   public function view($id) {
       $post = Cache::read('post_' . $id, 'posts');
       if (!$post) {
           $post = $this->Post->findById($id);
           Cache::write('post_' . $id, $post, 'posts');
       }
       $this->set('post', $post);
   }
   ```

## Cache Clearing

1. **Clear Specific Cache**
   ```php
   Cache::delete('posts_index');
   Cache::delete('post_1', 'posts');
   ```

2. **Clear All Cache**
   ```php
   Cache::clear();
   Cache::clear(false, 'posts');
   ```

## Best Practices

1. **Cache Strategy**
   - Cache expensive operations
   - Use appropriate duration
   - Clear cache when needed
   - Monitor cache size

2. **Performance**
   - Use appropriate engine
   - Monitor hit rates
   - Balance memory usage
   - Regular maintenance

3. **Maintenance**
   - Document cache keys
   - Version control config
   - Regular review
   - Update as needed

4. **Security**
   - Secure cache storage
   - Validate cache data
   - Handle sensitive data
   - Regular security review 