PDODblibBundle
--------------

Doctrine 2 does support any method of connecting to SQL Server on a Linux box. Here's a simple driver that supports PDO DBlib. It's pretty rough.

This bundle requires the following:
* pdo_dblib
* FreeTDS

Since Doctrine 2 not allow you to add custom database drivers on the fly. Modify `Doctrine/DBAL/Driver/DriverManager::$_driverMap` as follows:

```php
final class DriverManager
{
    private static $_driverMap = array(
		/* ... snip ... */
        'pdo_dblib' => 'Doctrine\DBAL\Driver\PDODblib\Driver',
    );
}
```

In your Symfony2 project, modify your `config.yml` as follows:

```yml
# Doctrine Configuration
doctrine:
    dbal:
        driver:         pdo_dblib
        driver_class:   PDODblibBundle\Doctrine\DBAL\Driver\PDODblib\Driver
```