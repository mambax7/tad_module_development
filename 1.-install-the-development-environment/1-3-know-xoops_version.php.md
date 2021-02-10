# 1-3 Know xoops\_version.php



#### 1. Modify the settings in xoops\_version.php in order

1. There must be a xoops\_version.php configuration file in the XOOPS module directory, otherwise it is not a standard module.
2. Please follow the configuration file sequence to generate relative files.

   ```text
   <?php
   $modversion = array();

   //---模組基本資訊---//
   $modversion['name']        = '活動報名';
   $modversion['version']     = 1.00;
   $modversion['description'] = '簡易的活動報名系統';
   $modversion['author']      = 'Tad';
   $modversion['credits']     = '';
   $modversion['help']        = 'page=help';
   $modversion['license']     = 'GNU GPL 2.0';
   $modversion['license_url'] = 'www.gnu.org/licenses/gpl-2.0.html/';
   $modversion['image']       = 'images/logo.png';
   $modversion['dirname']     = basename(dirname(__FILE__));

   //---模組狀態資訊---//
   $modversion['release_date']        = '2017/08/05';
   $modversion['module_website_url']  = 'http://www.tad0616.net';
   $modversion['module_website_name'] = 'Tad教材網';
   $modversion['module_status']       = 'release';
   $modversion['author_website_url']  = 'http://www.tad0616.net';
   $modversion['author_website_name'] = 'Tad教材網';
   $modversion['min_php']             = 5.4;
   $modversion['min_xoops']           = '2.5';
   $modversion['min_tadtools']        = '1.20';

   //---paypal資訊---//
   $modversion['paypal']                  = array();
   $modversion['paypal']['business']      = 'tad@gmail.com';
   $modversion['paypal']['item_name']     = 'Donation : ' . 'Tad';
   $modversion['paypal']['amount']        = 10;
   $modversion['paypal']['currency_code'] = 'USD';

   //---後台使用系統選單---//
   $modversion['system_menu'] = 1;
   ```

   |  |  |
   | :--- | :--- |

3. $modversion\['version'\] The version number can be written as 1.0, 2.3..., but 1.0.1 needs to be written as 1.01.
4. $modversion\['module\_status'\] module status can be Alpha, Beta, RC, Release
5. $modversion\['min\_tadtools'\] is our own new setting. If the module must be matched with tadtools of a certain version or higher, it is necessary.
   * 

#### 2. Language in xoops\_version.php

1. If xoops\_version.php is useful for Chinese, it is recommended to make a language file.
2. If it's just for personal use, you can write it in Chinese directly \(the string must be quoted\), but the $modversion\['config'\] preference setting must use the language.
3. The language file of xoops\_version.php is always located in language/tchinese\_utf8/modinfo.php \(you cannot customize the file or change the file name\)
4. Language setting method: define\("\_MI\_ language name", "corresponding actual Chinese"\);
5. "\_MI\_Language name" is a PHP constant, and \_MI is the beginning of a constant suggested by XOOPS. Generally speaking, it is recommended to start with an underscore and use all capitals for easy identification \(but it is not mandatory\).
6. Generally, the module name will be added after \_MI to avoid constant conflicts, for example: \_MI\_MYMOD\_XXX

   ```text
   define('_MI_SIGNUP_NAME', '活動報名');
   define('_MI_SIGNUP_DESCRIPTION', '簡易的活動報名系統');
   define('_MI_SIGNUP_MODULE_WEBSITE_NAME', 'Tad教材網');
   define('_MI_SIGNUP_AUTHOR_WEBSITE_NAME', 'Tad教材網');
   ```

   |  |
   | :--- |

7. The content of xoops\_version.php will become like this:

   ```text
   <?php
   $modversion = array();

   //---模組基本資訊---//
   $modversion['name']        = _MI_SIGNUP_NAME;
   $modversion['version']     = 1.00;
   $modversion['description'] = _MI_SIGNUP_DESCRIPTION;
   $modversion['author']      = 'Tad';
   $modversion['credits']     = '';
   $modversion['help']        = 'page=help';
   $modversion['license']     = 'GNU GPL 2.0';
   $modversion['license_url'] = 'www.gnu.org/licenses/gpl-2.0.html/';
   $modversion['image']       = 'images/logo.png';
   $modversion['dirname']     = basename(dirname(__FILE__));

   //---模組狀態資訊---//
   $modversion['release_date']        = '2017/08/05';
   $modversion['module_website_url']  = 'http://www.tad0616.net';
   $modversion['module_website_name'] = _MI_SIGNUP_MODULE_WEBSITE_NAME;
   $modversion['module_status']       = 'release';
   $modversion['author_website_url']  = 'http://www.tad0616.net';
   $modversion['author_website_name'] = _MI_SIGNUP_AUTHOR_WEBSITE_NAME;
   $modversion['min_php']             = 5.4;
   $modversion['min_xoops']           = '2.5';
   $modversion['min_tadtools']        = '1.20';
   ```

