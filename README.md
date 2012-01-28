PDODblibBundle
--------------

Doctrine 2 does support any method of connecting to SQL Server on a Linux box. Here's a simple driver that supports PDO DBlib. Many tests fail, but most are related to shortcomings of the PDODBlib driver. There is a patch in the PHP repo to add transaction and lastInsertId support, but this package has some minor work arounds.

This bundle requires the following:
* pdo_dblib
* FreeTDS

Since Doctrine 2 not allow you to add custom database drivers on the fly, if you want to test this package, `Doctrine/DBAL/Driver/DriverManager::$_driverMap` as follows:

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
        driver_class:   PDODblibBundle\Doctrine\DBAL\Driver\PDODblib\Driver
```

PHP pdo_dblib patch
===================

You can find a patch for some of the short-comings of pdo_dblib on SVN.

http://svn.php.net/viewvc/php/php-src/trunk/ext/pdo_dblib/dblib_driver.c?view=log

See:
Revision 300647 - lastInsertId
Revision 300628 - transaction support