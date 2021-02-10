# 6-6 Display list

#### 1. List all activities

1. When listing all activities, first make a basic filter to filter out:
   * There are activities enabled \(enable=1\)
   * In theory, the activities whose deadlines have not arrived should still be displayed, but they cannot be registered.
2. In addition, when sorting, it is hoped that the activities that are approaching the deadline will be presented first, so the deadline is used for the reverse descending order.
3. The entire syntax is as follows:

   ```text
   //顯示活動列表
   function list_action()
   {
       global $xoopsDB, $xoopsTpl;

       $tbl    = $xoopsDB->prefix('actions');
       $sql    = "SELECT * FROM `{$tbl}` WHERE `enable` ='1' ORDER BY `end_date` DESC";
       $result = $xoopsDB->query($sql) or web_error($sql);
       while ($action = $xoopsDB->fetchArray($result)) {
           $actions[] = $action;
       }
       $xoopsTpl->assign('actions', $actions);
   }
   ```

#### 2. Modify tad\_signup\_index.tpl template file

1. Edit templates/tad\_signup\_index.tpl and add the following syntax:

   ```text
   <{if $op=="list_action"}>
     <h2>所有活動列表</h2>
     <table class="table table-bordered table-hover table-striped">
       <thead>
         <tr class="info">
           <th>活動名稱</th>
           <th>活動日期</th>
           <th>報名截止日</th>
           <th>功能</th>
         </tr>
       </thead>
       <tbody>
       <{foreach from=$actions item=action}>
         <tr>
           <td><a href="index.php?action_id=<{$action.action_id}>"><{$action.title}></a></td>
           <td><{$action.action_date}></td>
           <td><{$action.end_date}></td>
           <td>
             <a href="index.php?action_id=<{$action.action_id}>" class="btn btn-info btn-xs">詳情</a>
           </td>
         </tr>
       <{foreachelse}>
         <tr>
           <td colspan=4>暫無活動</td>
         </tr>
       <{/foreach}>
       </tbody>
     </table>
   <{/if}>
   ```

