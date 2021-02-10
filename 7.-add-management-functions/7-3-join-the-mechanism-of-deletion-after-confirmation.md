# 7-3 Mechanism to delete after joining confirmation

1. First use the built-in sweet\_alert category of tadtools in the list\_action to generate the deleted js function, so as to make the "delete function after confirmation":

   ```text
   //顯示活動列表
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

       include_once XOOPS_ROOT_PATH . "/modules/tadtools/sweet_alert.php";
       $sweet_alert = new sweet_alert();
       $sweet_alert->render("delete_action", "admin/main.php?op=delete_action&action_id=", 'action_id');
   }
   ```

2. The first parameter of render\(\) is the name of the js delete function, the second parameter is the path to execute the deletion, and the last parameter is the number name passed in.
3. Edit the templates/tad\_signup\_index.tpl template and add the "Delete" button according to the identity

   ```text
   <td>
     <{if $isAdmin}>
       <a href="javascript:delete_action(<{$action.action_id}>)" class="btn btn-danger btn-xs">刪除</a>
       <a href="admin/main.php?action_id=<{$action.action_id}>" class="btn btn-warning btn-xs">編輯</a>
     <{/if}>
     <a href="index.php?action_id=<{$action.action_id}>" class="btn btn-info btn-xs">詳情</a>
   </td>
   ```

