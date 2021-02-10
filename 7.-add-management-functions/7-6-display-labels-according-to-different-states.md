# 7-6 Display labels according to different states

1. Because the interface of the administrator and the user has been adjusted in the previous unit, the administrator can see the closed and expired information. Therefore, the administrator must know which data is closed and which data has expired, so as not to recognize There is a conflict between the above and the user.
2. The closed information can directly modify the /templates/tad\_signup\_index.tpl template to do:

   ```text
   <{if $action.enable!=1}>
     <span class="label label-danger">已關閉</span>
   <{/if}>  
   ```

3. In addition, the expired date needs to be compared, so handle it in index.php

   ```text
   //顯示預設頁面內容
   function list_actions()
   {
       global $xoopsTpl, $xoopsDB, $isAdmin;

       $tbl=$xoopsDB->prefix('actions');

       $where=$isAdmin?'':"WHERE `enable` = '1' and `end_date` > NOW()";

       $sql="SELECT * FROM `{$tbl}` $where ORDER BY `end_date` DESC";
       //送至資料庫
       $result = $xoopsDB->query($sql) or web_error($sql);
       //取回資料
       $actions=[];
       $myts              = MyTextSanitizer::getInstance();
       while($action=$xoopsDB->fetchArray($result)){
           $action['title']   = $myts->htmlSpecialChars($action['title']);
           $action['content'] = $myts->displayTarea($action['content'], 1, 1, 1, 1, 0);    
           $action['overdue'] = time() > strtotime($action['end_date'])?1:0;
           $actions[]=$action;
       }

       $xoopsTpl->assign('actions', $actions);

       include_once XOOPS_ROOT_PATH . "/modules/tadtools/sweet_alert.php";
       $sweet_alert = new sweet_alert();
       $sweet_alert->render("delete_action", "admin/main.php?op=delete_action&action_id=", 'action_id');
   }
   ```

4. Then go to modify the /templates/tad\_signup\_index.tpl template and add the corresponding treatment:

   ```text
   <{if $action.overdue}>
     <span class="label label-warning">已過期</span>
   <{/if}> 
   ```

