# 4-8 automatic function



1. It doesn't matter if this item is not. It is mainly used to set some specific actions to be performed by the way when installing \(or uninstalling\) the module. It is not commonly used \(and there is no requirement that it must be placed in the include\).
2. onInstall is the program to be executed when the module is installed. The file must contain a function: xoops\_module\_install\_module directory, this function will be executed when the module is installed. Below are the four folders needed by CKEditor to be automatically created when the module is installed.

   ```text
   <?php
   function xoops_module_install_tad_signup(&$module) {
       mk_dir(XOOPS_ROOT_PATH . "/uploads/tad_signup");
       mk_dir(XOOPS_ROOT_PATH . "/uploads/tad_signup/file");
       mk_dir(XOOPS_ROOT_PATH . "/uploads/tad_signup/image");
       mk_dir(XOOPS_ROOT_PATH . "/uploads/tad_signup/image/.thumbs");
       return true;
   }

   ...底下略...
   ```

3. onUninstall is the program to be executed when the module is removed. The file must contain a function: xoops\_module\_uninstall\_module directory, this function will be executed when the module is uninstalled.
4. onUpdate is the program to be executed when the module is updated. The file must contain a function: xoops\_module\_update\_module directory, this function will be executed when the module is updated. Below are the four folders needed by CKEditor to be automatically created when the module is installed.

   ```text
   <?php

   function xoops_module_update_tad_signup(&$module, $old_version) {
       GLOBAL $xoopsDB;
       mk_dir(XOOPS_ROOT_PATH . "/uploads/tad_signup");
       mk_dir(XOOPS_ROOT_PATH . "/uploads/tad_signup/file");
       mk_dir(XOOPS_ROOT_PATH . "/uploads/tad_signup/image");
       mk_dir(XOOPS_ROOT_PATH . "/uploads/tad_signup/image/.thumbs");
   		//if(!chk_chk1()) go_update1();

       return true;
   }

   ...底下略...
   ```

5. When using it, please remove the annotations of the sample files inside. If you need an example, please refer to its writing in each public module, especially the part of adding a field or adding a table, which is very common.

