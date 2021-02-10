# 6-9 Add to the module toolbar



#### 1. Add the module toolbar

1. The module toolbar is provided by tadtools, and its syntax is as follows, just add it directly before the end of the page:

   ```text
   /*-----------秀出結果區--------------*/
   $xoopsTpl->assign('op', $op);
   $xoopsTpl->assign("toolbar", toolbar_bootstrap($interface_menu));
   include_once XOOPS_ROOT_PATH . '/footer.php';
   ```

2. Then add the &lt;{$toolbar}&gt; template tag to the most square of the template file templates/tad\_signup\_index.tpl at the front desk.

#### 2. About interface\_menu.php

1. The options of the menu are set in interface\_menu.php.
2. If the interface\_menu.php file exists, XOOPS will integrate all the options into the navigation bar.
3. In other words, if you don't want this module option to appear on the inverted column, please copy the content of interface\_menu.php to header.php \(and delete or replace the include\_once "interface\_menu.php"; line\).

#### Three, setting options

1. The options are:

   ```text
   $interface_menu[_TAD_TO_MOD] = "index.php";
   $interface_icon[_TAD_TO_MOD] = "fa-chevron-right";
   ```

2. \_TAD\_TO\_MOD can be written in Chinese directly, and then it will become the option name.
3. $interface\_menu\[option name\] is to set the page of the module when the option is pressed.
4. $interface\_icon\[option name\] is the icon on the left to set the option, using [font-awesome](http://fontawesome.io/icons/) .

