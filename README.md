Doctrine 2 does support any method of connecting to SQL Server on a Linux box. Here's a simple driver that supports PDO DBlib. It's pretty rough.



Since Doctrine 2 not allow you to add custom database drivers on the fly. So you must modify Doctrine/DBAL/Driver/DriverManager::$_driverMap as follows:

final class DriverManager
{
    private static $_driverMap = array(
		/* ... snip ... */
        'pdo_dblib' => 'Doctrine\DBAL\Driver\PDODblib\Driver', // Added this line
    );
}
