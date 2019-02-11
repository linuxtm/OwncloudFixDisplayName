# MySQL trigger to fix ownCloud display_name
Fix display_name in owncloud with Zimbra Drive integration

```
DELIMITER $$
USE `owncloud`$$
CREATE DEFINER=`root`@`localhost` TRIGGER `owncloud`.`oc_accounts_BEFORE_UPDATE` BEFORE UPDATE ON `oc_accounts` FOR EACH ROW
BEGIN
	SET NEW.display_name=OLD.email;
    
END$$
DELIMITER ;
```
