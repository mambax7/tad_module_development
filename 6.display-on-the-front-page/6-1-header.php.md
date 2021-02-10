# 6-1 header.php

Copy the content of interface\_menu.php to the header.php and delete interface\_menu.php

```text
<?php
//Load XOOPS main profile (required)
include_once "../../mainfile.php";
//Load custom common function file
include_once "function.php";
//Load the tool menu configuration file (you can also copy the content of interface_menu.php below this file and delete interface_menu.php)

//Determine whether the module has management authority
$isAdmin == false;
if ($xoopsUser) {
    $isAdmin   = $xoopsUser->isAdmin($module_id);
}

//Toolbar settings

//Back to module homepage
$interface_menu[_TAD_TO_MOD] = "index.php";
$interface_icon[_TAD_TO_MOD] = "fa-chevron-right";

//Module background
if ($isAdmin) {
    $interface_menu[_TAD_TO_ADMIN] = "admin/main.php";
    $interface_icon[_TAD_TO_ADMIN] = "fa-chevron-right";
}
```

