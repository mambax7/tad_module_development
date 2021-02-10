# 11-1 Add tabs and apply preferences



1. Modify the paging settings in list\_action\(\) in index.php

   ```text
   //顯示活動列表
   function list_action()
   {
       global $xoopsDB, $xoopsTpl, $isAdmin, $xoopsModuleConfig;

       $tbl   = $xoopsDB->prefix('actions');
       $where = $isAdmin ? '' : "WHERE `enable` ='1' AND `end_date` > now() ";
       $sql   = "SELECT * FROM `{$tbl}` $where ORDER BY `end_date` DESC";

       //getPageBar($原sql語法, 每頁顯示幾筆資料, 最多顯示幾個頁數選項);
       $PageBar = getPageBar($sql, $xoopsModuleConfig['display_amount'], 10);
       $bar     = $PageBar['bar'];
       $sql     = $PageBar['sql'];
       $total   = $PageBar['total'];
       $xoopsTpl->assign('bar', $bar);
       $xoopsTpl->assign('total', $total);
       ...略...
   }
   ```

2. $xoopsModuleConfig\['display\_amount'\] can replace the number of pages. If in the function, remember to global $xoopsModuleConfig;
3. Also remember to set the language file.

