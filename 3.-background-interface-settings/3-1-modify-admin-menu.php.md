# 3-1 Modify admin/menu.php



1. This is used to define the home page of the admin/index.php module backend and the content link to appear in the module console menu.
2. The main thing is to modify this part. If there is a second page, please add one by yourself:

   ```text
   $i++;
   $adminmenu[$i]['title'] = _MI_TAD_SIGNUP_ADMENU1;
   $adminmenu[$i]['link']  = "admin/main.php";
   $adminmenu[$i]['desc']  = _MI_TAD_SIGNUP_ADMENU1_DESC;
   $adminmenu[$i]['icon']  = 'images/admin/button.png';
   ```

3. Among them, admin/main.php is the page we intend to use to open events. \(This file also has a default\)
   * title is the title to set the link, "\_MI\_TAD\_SIGNUP\_ADMENU1" is the language constant, which must be defined in language/tchinese\_utf8/modinfo.php with a constant.
   * link is the file link
   * dese describes the purpose of the page
   * icon is used to set the button pattern of the link \(images/admin/button.png is built-in, you can also download the 32x32 icon from [https://www.flaticon.com/](https://www.flaticon.com/) to use\)
4. Edit language file language/tchinese\_utf8/modinfo.php

   ```text
   <?php
   include_once XOOPS_ROOT_PATH . "/modules/tadtools/language/{$xoopsConfig['language']}/modinfo_common.php";

   define("_MI_TAD_SIGNUP_ADMENU1", "活動管理");
   define("_MI_TAD_SIGNUP_ADMENU1_DESC", "後台活動管理");
   ```

