# 6-8 Filter all read functions



1. Filter show\_action function

   ```text
   //Show single event
   function show_action($action_id)
   {
       global $xoopsDB, $xoopsTpl;
       $tbl               = $xoopsDB->prefix('actions');
       $sql               = "SELECT * FROM `{$tbl}` WHERE `action_id` ='{$action_id}'";
       $result            = $xoopsDB->query($sql) or web_error($sql);
       $action            = $xoopsDB->fetchArray($result);
       $myts              = MyTextSanitizer::getInstance();
       $action['title']   = $myts->htmlSpecialChars($action['title']);
       $action['content'] = $myts->displayTarea($action['content'], 1, 1, 1, 1, 0);
       $xoopsTpl->assign('action', $action);
   }
   ```

2. Filter list\_action function

   ```text
   //Show event list
   function list_action()
   {
       global $xoopsDB, $xoopsTpl;

       $tbl    = $xoopsDB->prefix('actions');
       $sql    = "SELECT * FROM `{$tbl}` WHERE `enable` ='1' AND `end_date` > now() ORDER BY `end_date` DESC";
       $result = $xoopsDB->query($sql) or web_error($sql);
       $myts   = MyTextSanitizer::getInstance();
       while ($action = $xoopsDB->fetchArray($result)) {
           $action['title']   = $myts->htmlSpecialChars($action['title']);
           $action['content'] = $myts->displayTarea($action['content'], 1, 1, 1, 1, 0);
           $actions[]         = $action;
       }
       $xoopsTpl->assign('actions', $actions);
   }
   ```

