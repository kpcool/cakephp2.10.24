# Internationalization

This guide covers internationalization (i18n) and localization (l10n) in CakePHP 2.x.

## Configuration

1. **App Configuration**
   ```php
   // app/Config/core.php
   Configure::write('Config.language', 'eng');
   ```

2. **Locale Configuration**
   ```php
   // app/Config/bootstrap.php
   setlocale(LC_ALL, 'en_US.UTF-8');
   ```

## Translation Files

1. **Default Domain**
   ```php
   // app/Locale/eng/LC_MESSAGES/default.po
   msgid "Hello"
   msgstr "Hello"
   ```

2. **Custom Domain**
   ```php
   // app/Locale/eng/LC_MESSAGES/custom.po
   msgid "Welcome"
   msgstr "Welcome"
   ```

## Translation Functions

1. **Basic Translation**
   ```php
   // In views
   echo __("Hello World");
   echo __d('custom', "Welcome");
   ```

2. **Plural Forms**
   ```php
   // In views
   echo __n("%d item", "%d items", $count, $count);
   echo __dn('custom', "%d user", "%d users", $count, $count);
   ```

## Date and Time

1. **Date Formatting**
   ```php
   // In views
   echo $this->Time->format($date, '%B %e, %Y');
   echo $this->Time->format($date, '%c');
   ```

2. **Time Zones**
   ```php
   // In controllers
   date_default_timezone_set('UTC');
   ```

## Number Formatting

1. **Currency**
   ```php
   // In views
   echo $this->Number->currency($amount, 'USD');
   echo $this->Number->currency($amount, 'EUR');
   ```

2. **Decimal Numbers**
   ```php
   // In views
   echo $this->Number->format($number, array('places' => 2));
   echo $this->Number->format($number, array('before' => '€'));
   ```

## Best Practices

1. **Translation Files**
   - Keep translations organized
   - Use meaningful keys
   - Maintain consistency
   - Regular updates

2. **Code Organization**
   - Use translation domains
   - Group related strings
   - Document context
   - Version control

3. **Performance**
   - Cache translations
   - Minimize string concatenation
   - Use appropriate functions
   - Regular optimization

4. **Maintenance**
   - Regular reviews
   - Update documentation
   - Test all languages
   - Backup translations 