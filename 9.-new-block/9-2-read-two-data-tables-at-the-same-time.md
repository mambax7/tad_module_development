# 9-2 Read two data tables at the same time

#### 1. Use join to read more than two data tables at once

1. The convenience of the associated data table is that more than two data tables can be read at a time. The simple syntax is as follows:

   ```text
   SELECT a.* , b.* , c.*
   FROM `資料表1` as a
   JOIN `資料表2` as b ON a.`索引欄位`= b.`索引欄位`
   JOIN `資料表3` as c ON b.`索引欄位`= c.`索引欄位`
   WHERE a.欄位='值' AND ….
   ```

2. "Left join" means to focus on the left, and by the way, go to the right to see if there is any specified data.
3. "Right join" means that the right is the main one. By the way, go to the left to see if there is any specified data.
4. "Join" means that both sides must have data at the same time, otherwise the data will not appear.
5. In this example, read out the applicant's number, and by the way read out the writing of the applicant's information:

   ```text
   //區塊主函數：列出所報者
   function list_signup($options)
   {
       global $xoopsDB;
       if ($_GET['action_id']) {
           $signups_tbl = $xoopsDB->prefix('signups');
           $users_tbl   = $xoopsDB->prefix('users');
           $action_id   = intval($_GET['action_id']);
           $sql         = "SELECT a.*, b.* FROM `{$signups_tbl}` AS a
           JOIN `{$users_tbl}` as b ON a.`uid` = b.`uid`
           WHERE a.`action_id` = '{$action_id}'";
           $result  = $xoopsDB->query($sql) or web_error($sql);
           $signups = [];
           while ($val = $xoopsDB->fetchArray($result)) {
               $signups[] = $val;
           }
           return $signups;
       }
   }
   ```

6. Join here means that there must be member information, otherwise it will not be shown.

#### 2. Modify the template

1. Modify \templates\side\_signups.tpl and change uid to name. Add Email here by the way

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
   ```

