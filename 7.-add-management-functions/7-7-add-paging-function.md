# 7-7 add paging function

1. Pagination is also a built-in function of tadtools, which can be added directly between the $sql syntax and the send request:

   ```text
   //顯示預設頁面內容
   function list_actions()
   {
       global $xoopsTpl, $xoopsDB, $isAdmin;

       $tbl=$xoopsDB->prefix('actions');

       $where=$isAdmin?'':"WHERE `enable` = '1'";

       $sql="SELECT * FROM `{$tbl}` $where ORDER BY `end_date` DESC";
    
       //getPageBar($原sql語法, 每頁顯示幾筆資料, 最多顯示幾個頁數選項);
       $PageBar = getPageBar($sql, 5, 10);
       $bar     = $PageBar['bar'];
       $sql     = $PageBar['sql'];
       $total   = $PageBar['total'];
       $xoopsTpl->assign('bar', $bar);
       $xoopsTpl->assign('total', $total);

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

2. The obtained $bar is the toolbar, and $total is the total number of data. We can send the two variables Jiangsu and Zhejiang to the template for use, so modify templates/tad\_signup\_index.tpl and add:

   ```text
   <{if $op=="list_actions"}>
     <h2>活動列表<small>（共 <{$total}> 個活動）</small></h2>
     <table class="table table-bordered table-hover table-striped">
       <tr class="info">
         <th>活動日期</th>
         <th>活動名稱</th>
         <th>截止日期</th>
         <th>功能</th>
       </tr>
       <{foreach from=$actions item=action}>
         <tr>
           <td><{$action.action_date}></td>
           <td>
             <{if $action.enable!=1}>
               <span class="label label-danger">已關閉</span>
             <{/if}>  

             <{if $action.overdue}>
               <span class="label label-warning">已過期</span>
             <{/if}> 
             <a href="index.php?action_id=<{$action.action_id}>"><{$action.title}></a>
           </td>
           <td><{$action.end_date}></td>
           <td>
             <{if $isAdmin}>
               <a href="javascript:delete_action(<{$action.action_id}>)" class="btn btn-danger btn-xs">刪除</a>
               <a href="admin/main.php?action_id=<{$action.action_id}>" class="btn btn-warning btn-xs">編輯</a>
             <{/if}>
             <a href="index.php?action_id=<{$action.action_id}>" class="btn btn-info btn-xs">詳情</a>
           </td>
         </tr>
       <{/foreach}>
     </table>
     <{$bar}>
   <{/if}>
   ```

