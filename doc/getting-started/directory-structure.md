# Directory Structure

This guide explains the standard directory structure of a CakePHP 2.x application.

## Root Directory

```
app/                # Application directory
lib/                # CakePHP core libraries
plugins/            # Plugin directory
vendors/            # Third-party libraries
```

## Application Directory (app/)

The `app` directory contains your application's specific files and directories:

```
app/
├── Config/         # Configuration files
│   ├── core.php    # Core configuration
│   ├── bootstrap.php  # Application bootstrap
│   ├── routes.php  # URL routing configuration
│   ├── database.php  # Database configuration
│   └── email.php   # Email configuration
│
├── Console/        # Console commands
│   ├── Command/    # Console commands
│   └── Templates/  # Console templates
│
├── Controller/     # Controllers
│   ├── Component/  # Components
│   └── AppController.php  # Base controller
│
├── Lib/            # Application libraries
│
├── Locale/         # Internationalization files
│   └── [lang]/     # Language files
│
├── Model/          # Models
│   ├── Behavior/   # Model behaviors
│   └── Datasource/ # Data sources
│
├── Plugin/         # Application plugins
│
├── tmp/            # Temporary files
│   ├── cache/      # Cache files
│   ├── logs/       # Log files
│   └── sessions/   # Session files
│
├── View/           # Views
│   ├── Elements/   # View elements
│   ├── Errors/     # Error pages
│   ├── Helper/     # View helpers
│   ├── Layouts/    # Layouts
│   └── [Controller]/  # Controller views
│
└── webroot/        # Public files
    ├── css/        # CSS files
    ├── img/        # Image files
    ├── js/         # JavaScript files
    └── index.php   # Front controller
```

## Core Libraries Directory (lib/)

The `lib` directory contains the CakePHP core:

```
lib/
├── Cake/           # CakePHP core
│   ├── Cache/      # Caching
│   ├── Config/     # Configuration
│   ├── Console/    # Console
│   ├── Controller/ # Core controllers
│   ├── Core/       # Core functionality
│   ├── Error/      # Error handling
│   ├── Event/      # Events
│   ├── I18n/       # Internationalization
│   ├── Log/        # Logging
│   ├── Model/      # Core models
│   ├── Network/    # Networking
│   ├── Routing/    # Routing
│   ├── Test/       # Testing
│   ├── Utility/    # Utilities
│   ├── View/       # Core views
│   └── bootstrap.php  # Core bootstrap
│
└── CakePHP/        # Framework files
```

## Plugin Directory (plugins/)

The `plugins` directory contains installed plugins:

```
plugins/
└── [PluginName]/
    ├── Config/     # Plugin configuration
    ├── Console/    # Plugin console commands
    ├── Controller/ # Plugin controllers
    ├── Locale/     # Plugin translations
    ├── Model/      # Plugin models
    ├── View/       # Plugin views
    └── webroot/    # Plugin public files
```

## Vendors Directory (vendors/)

The `vendors` directory contains third-party libraries:

```
vendors/
└── [LibraryName]/  # Third-party libraries
```

## Important Files

1. **app/Config/core.php**
   - Core configuration settings
   - Debug mode
   - Security settings
   - Cache configuration

2. **app/Config/database.php**
   - Database connection settings
   - Multiple database configurations

3. **app/Config/routes.php**
   - URL routing rules
   - Custom routes

4. **app/Config/bootstrap.php**
   - Application bootstrap
   - Custom initialization

5. **app/View/Layouts/default.ctp**
   - Default layout template
   - Common HTML structure

6. **app/Controller/AppController.php**
   - Base controller class
   - Common controller functionality

7. **app/Model/AppModel.php**
   - Base model class
   - Common model functionality

## Best Practices

1. **File Organization**:
   - Keep related files together
   - Follow naming conventions
   - Use meaningful names

2. **Directory Structure**:
   - Don't modify core directories
   - Keep custom code in appropriate directories
   - Use plugins for reusable code

3. **Configuration**:
   - Keep sensitive data in configuration files
   - Use environment-specific configurations
   - Document configuration changes

4. **Temporary Files**:
   - Keep tmp directory clean
   - Configure proper permissions
   - Set up log rotation 