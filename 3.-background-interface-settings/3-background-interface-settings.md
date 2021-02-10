# 3 Background interface settings



1. Whether the module needs a background, you can set it in xoops\_version.php

   ```text
   //---後台管理介面設定---//
   $modversion['hasAdmin']   = 1;
   $modversion['adminindex'] = 'admin/index.php';
   $modversion['adminmenu']  = 'admin/menu.php';
   ```

2. The value of $modversion\['hasAdmin'\] is set to 1 to have a background.
3. $modversion\['adminindex'\] is the main index page of the setting backend \(used to display the link button\), basically index.php is already built-in, so you don't need to write it yourself.
4. $modversion\['adminmenu'\] is used to generate menus for the background console.



