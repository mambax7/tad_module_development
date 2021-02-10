# 2-1 Complete part of the database setting



#### 1. Export data table

1. Click "Export" on the left to save the file as [sql/mysql.sql](https://campus-xoops.tn.edu.tw/uploads/tad_book3/file/29/mysql.sql) file.
2. [sql is a plain text file](https://campus-xoops.tn.edu.tw/uploads/tad_book3/file/29/mysql.sql) , which can be used to import in the future to quickly build a database structure, and the comments and suggestions in it are deleted.

#### 2. Modify the settings of xoops\_version.php

1. Edit xoops\_version.php, uncomment the database setting part, and fill in the correct content

   ```text
   //---模組資料表架構---//
   $modversion['sqlfile']['mysql'] = 'sql/mysql.sql';
   $modversion['tables'][]         = 'actions';
   $modversion['tables'][]         = 'signups';
   ```

2. $modversion\['sqlfile'\]\['mysql'\] is used during installation
3. $modversion\['tables'\] is used when uninstalling



