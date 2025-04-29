# Basic Setup

This guide will help you set up your first CakePHP 2.x application.

## Directory Structure

CakePHP follows a convention over configuration approach. Here's the basic directory structure:

```
app/
├── Config/          # Configuration files
├── Console/         # Console commands
├── Controller/      # Controllers
├── Lib/            # Libraries
├── Locale/         # Internationalization files
├── Model/          # Models
├── Plugin/         # Plugins
├── tmp/            # Temporary files
├── View/           # Views
└── webroot/        # Public files
```

## Configuration Files

### Core Configuration

The main configuration file is `app/Config/core.php`. Important settings include:

```php
Configure::write('debug', 2);  // Development mode
Configure::write('Security.salt', 'YOUR-SALT-HERE');
Configure::write('Security.cipherSeed', 'YOUR-CIPHER-SEED-HERE');
```

### Database Configuration

Configure your database in `app/Config/database.php`:

```php
class DATABASE_CONFIG {
    public $default = array(
        'datasource' => 'Database/Mysql',
        'persistent' => false,
        'host' => 'localhost',
        'login' => 'user',
        'password' => 'password',
        'database' => 'database_name',
        'prefix' => '',
        'encoding' => 'utf8'
    );
}
```

## Creating Your First Controller

1. Create a new file in `app/Controller/PagesController.php`:

```php
class PagesController extends AppController {
    public function display() {
        $path = func_get_args();
        $count = count($path);
        if (!$count) {
            return $this->redirect('/');
        }
        $page = $subpage = $title = null;

        if (!empty($path[0])) {
            $page = $path[0];
        }
        if (!empty($path[1])) {
            $subpage = $path[1];
        }
        if (!empty($path[$count - 1])) {
            $title = Inflector::humanize($path[$count - 1]);
        }
        $this->set(compact('page', 'subpage', 'title'));
    }
}
```

## Creating Your First View

1. Create a new file in `app/View/Pages/home.ctp`:

```php
<h1>Welcome to CakePHP</h1>
<p>This is your first CakePHP application.</p>
```

## Routing

Basic routing is configured in `app/Config/routes.php`:

```php
Router::connect('/', array('controller' => 'pages', 'action' => 'display', 'home'));
```

## Development Tools

CakePHP comes with several development tools:

1. **Debug Kit**: A debugging toolbar
2. **Console**: Command-line tools for development
3. **Bake**: Code generation tool

To use Bake:

```bash
cd /path/to/your/app
Console/cake bake
```

## Best Practices

1. **Follow Conventions**:
   - Use plural form for table names
   - Use singular form for model names
   - Use CamelCase for class names
   - Use lowercase for file names

2. **Security**:
   - Always validate input
   - Use prepared statements
   - Implement CSRF protection
   - Use proper authentication

3. **Performance**:
   - Enable caching
   - Optimize database queries
   - Use proper indexing
   - Minimize database calls

4. **Code Organization**:
   - Keep controllers thin
   - Put business logic in models
   - Use components for shared functionality
   - Use helpers for view logic 