# 9-4 Adjust the block according to the block setting

1. Then edit the main function list\_signup\($options\) in blocks/list\_signup.php, mainly to bring in the set values.

   ```text
   //區塊主函數：列出所報者
   function list_signup($options)
   {
       global $xoopsDB;
       if ($_GET['action_id']) {
           $signups['show_button'] = $options[0];
           if ($options[0] == 1) {
               include_once XOOPS_ROOT_PATH . "/modules/tadtools/sweet_alert.php";
               $sweet_alert = new sweet_alert();
               $sweet_alert->render("delete_signup", XOOPS_URL . "/modules/tad_signup/index.php?op=delete_signup&action_id=", 'action_id', "確定要取消嗎？", "取消後就不能參加活動囉！", "是！含淚取消！");
           }
           $signups_tbl          = $xoopsDB->prefix('signups');
           $users_tbl            = $xoopsDB->prefix('users');
           $action_id            = intval($_GET['action_id']);
           $signups['action_id'] = $action_id;
           $sql                  = "SELECT a.*, b.* FROM `{$signups_tbl}` AS a
           JOIN `{$users_tbl}` as b ON a.`uid` = b.`uid`
           WHERE a.`action_id` = '{$action_id}'";
           $result           = $xoopsDB->query($sql) or web_error($sql);
           $signups['users'] = [];
           while ($val = $xoopsDB->fetchArray($result)) {
               $signups['users'][] = $val;
           }
       }
       return $signups;
   }
   ```

2. Adjust the $signups array a bit, the first index value becomes the data type, so the list of applicants will become a four-dimensional array.
3. Modify the block template templates/blocks/list\_signup.tpl and make appropriate changes according to the passed variables.

   ```text
   <{if $block.action_id}>
     <table class="table table-hover table-striped">
       <thead>
         <tr class="info">
           <th>姓名</th>
           <th>Email</th>
         </tr>
       </thead>
       <tbody>
       <{foreach from=$block.users item=signup}>
           <tr>
             <td><{$signup.name}></td>
             <td><{$signup.email}></td>
           </tr>
       <{foreachelse}>
         <tr>
           <td colspan=2>暫無人報名</td>
         </tr>
       <{/foreach}>
       </tbody>
     </table>

     <{if $block.show_button and $xoops_isuser}>
       <{if $block.action_id|in_array:$smarty.session.uid_signup}>
         <a href="javascript:delete_signup(<{$block.action_id}>)" class="btn btn-danger btn-block">取消報名</a>
       <{else}>
         <a href="<{$xoops_url}>/modules/tad_signup/index.php?op=signup&action_id=<{$block.action_id}>" class="btn btn-success btn-block">我要報名</a>
       <{/if}>
     <{/if}>
   <{/if}>
   ```

