# 3-3 Background management homepage template



1. Modify the template file settings of main.php first

   ```text
   <?php
   /*-----------引入檔案區--------------*/
   $xoopsOption['template_main'] = "tad_signup_adm_main.tpl";
   include_once "header.php";
   include_once "../function.php";
   ```

2. The template name cannot be the same as other module names, so the general recommendation for naming is "module name\_background\_page name.tpl" to avoid duplication of file names. If it is in the foreground, just omit "\_background".
3. Then, please change templates/demo\_adm\_index.tpl to tad\_signup\_adm\_main.tpl.
4. Finally, open xoops\_version.php to modify the template settings

   ```text
   //---樣板設定---//
   $modversion['templates']                    = array();
   $i                                          = 1;
   $modversion['templates'][$i]['file']        = 'tad_signup_adm_main.tpl';
   $modversion['templates'][$i]['description'] = 'tad_signup_adm_main.tpl';
   ```

