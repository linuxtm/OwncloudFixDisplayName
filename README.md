# MySQL trigger to fix ownCloud display_name (will show full email address instead of user ID)
When using Zimbra Drive integration with ownCloud, the display name is randomly replaced by user's ID in ownCloud interface.
In order to fix it, you can set a mysql trigger to correct that and show user's email address. 
The trigger will update existing users when they first login after the trigger is in place.

For your convenience, you can directly wget the file with the trigger:
```
wget https://raw.githubusercontent.com/linuxtm/OwncloudFixUUID/master/mysql_trigger
```

Or you can copy it from below:
```
DELIMITER $$
USE `owncloud`$$
CREATE DEFINER=`root`@`localhost` TRIGGER `owncloud`.`oc_accounts_BEFORE_UPDATE` BEFORE UPDATE ON `oc_accounts` FOR EACH ROW
BEGIN
	SET NEW.display_name=OLD.email;
    
END$$
DELIMITER ;
```

You can also manually update the existing users, then let the MySQL trigger to prevent further modifications by running:
```
update oc_accounts set display_name=email where backend like '%ZimbraUsersBackend';
```
