# Routing

This guide covers routing in CakePHP 2.x.

## Basic Routing

1. **Default Routes**
   ```php
   // app/Config/routes.php
   Router::connect('/', array('controller' => 'pages', 'action' => 'display', 'home'));
   Router::connect('/pages/*', array('controller' => 'pages', 'action' => 'display'));
   ```

2. **Custom Routes**
   ```php
   // app/Config/routes.php
   Router::connect(
       '/blog/:year/:month/:day/:slug',
       array('controller' => 'posts', 'action' => 'view'),
       array(
           'pass' => array('year', 'month', 'day', 'slug'),
           'year' => '[12][0-9]{3}',
           'month' => '[01][0-9]',
           'day' => '[0-3][0-9]'
       )
   );
   ```

## Route Parameters

1. **Passed Parameters**
   ```php
   // app/Config/routes.php
   Router::connect(
       '/posts/:id',
       array('controller' => 'posts', 'action' => 'view'),
       array('id' => '[0-9]+')
   );
   ```

2. **Named Parameters**
   ```php
   // app/Config/routes.php
   Router::connect(
       '/posts/:id/:slug',
       array('controller' => 'posts', 'action' => 'view'),
       array(
           'id' => '[0-9]+',
           'slug' => '[a-zA-Z0-9-_]+'
       )
   );
   ```

## Route Prefixes

1. **Admin Prefix**
   ```php
   // app/Config/routes.php
   Router::connect('/admin/:controller/:action/*', array('prefix' => 'admin'));
   ```

2. **API Prefix**
   ```php
   // app/Config/routes.php
   Router::connect('/api/:controller/:action/*', array('prefix' => 'api'));
   ```

## RESTful Routing

1. **Resource Routes**
   ```php
   // app/Config/routes.php
   Router::mapResources('posts');
   Router::parseExtensions('json', 'xml');
   ```

2. **Custom REST Routes**
   ```php
   // app/Config/routes.php
   Router::connect(
       '/api/posts/:id',
       array(
           'controller' => 'posts',
           'action' => 'view',
           '[method]' => 'GET'
       ),
       array('id' => '[0-9]+')
   );
   ```

## Best Practices

1. **Route Design**
   - Use meaningful URLs
   - Follow REST conventions
   - Validate parameters
   - Document routes

2. **Performance**
   - Order routes efficiently
   - Use regex carefully
   - Cache routes
   - Monitor performance

3. **Maintenance**
   - Document changes
   - Version control
   - Regular review
   - Update as needed

4. **Security**
   - Validate parameters
   - Sanitize input
   - Check permissions
   - Regular security review 