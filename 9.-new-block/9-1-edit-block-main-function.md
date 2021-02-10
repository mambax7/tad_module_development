# 9-1 Edit block main function

#### One, modify the main function

1. Let's edit the main function list\_signup\(\) in blocks\list\_signup.php first, and its main purpose is to capture the content that is about to be presented in the area.

   ```text
   <?php
   //區塊主函數：列出所報者
   function list_signup($options)
   {
       global $xoopsDB;
       if ($_GET['action_id']) {
           $tbl       = $xoopsDB->prefix('signups');
           $action_id = intval($_GET['action_id']);
           $sql       = "SELECT * FROM `$tbl` where `action_id` = '{$action_id}'";
           $result    = $xoopsDB->query($sql) or web_error($sql);
           $signups   = [];
           while ($val = $xoopsDB->fetchArray($result)) {
               $signups[] = $val;
           }
           return $signups;
       }
   }
   ```

2. We use $\_GET\['action\_id'\] to get the current activity ID.
3. Then go to signups to retrieve all the registration records, make a three-dimensional array, and upload to the block template templates\blocks\list\_signup.tpl.
4. There is no need to go to assign\(\) specially, just return the variable. In the template, it will automatically be converted to &lt;{$block}&gt;.

#### 2. Modify the block template

1. Edit templates\blocks\list\_signup.tpl

   ```text
   <table class="table table-hover table-striped">
     <thead>
       <tr class="info">
         <th>姓名</th>
         <th>Email</th>
       </tr>
     </thead>
     <tbody>
     <{foreach from=$block item=signup}>
         <tr>
           <td><{$signup.uid}></td>
           <td><{$signup.signup_date}></td>
         </tr>
     <{foreachelse}>
       <tr>
         <td colspan=2>暫無人報名</td>
       </tr>
     <{/foreach}>
     </tbody>
   </table>
   ```

