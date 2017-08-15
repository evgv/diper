# Magento 2 folder/file permissions

 - The owner of the Magento file system: Must have full control (read/write/execute) of all files and directories.
 - Must not be the web server user; it should be a different user.
 - The web server user must have write access to the following files and directories: var app/etc pub
 - In addition, the web server's group must own the Magento file system so that the Magento user (who is in the group) can share access to files with the web server user. (This includes files created by the Magento Admin or other web-based utilities.)

###### We recommend setting the permissions as follows:
```sh
All directories have 770 permissions.

770 permissions give full control (that is, read/write/execute) to the owner and to the group and no permissions to anyone else.

All files have 660 permissions.

660 permissions mean the owner and the group can read and write but other users have no permissions.
```

###### You should set as bellow recommended.

```bash
cd <your Magento install dir> 

find . -type f -exec chmod 644 {} \;                        // 644 permission for files

find . -type d -exec chmod 755 {} \;                        // 755 permission for directory 

find ./var -type d -exec chmod 777 {} \;                // 777 permission for var folder    

find ./pub/media -type d -exec chmod 777 {} \;

find ./pub/static -type d -exec chmod 777 {} \;

chmod 777 ./app/etc

chmod 644 ./app/etc/*.xml

chown -R :<web server group> .

chmod u+x bin/magento
```


###### Short way
```bash

chown -R myuser:webservergroup /var/www/magento2/
chmod -R 755 /var/www/magento2/
chmod -R 777 /var/www/magento2/var/
chmod -R 777 /var/www/magento2/pub/

```
