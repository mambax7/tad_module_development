# 8-2 The interface changes after registration

1. In fact, after we have quietly registered for the built-in, we can no longer report the function! why? Because when we originally designed the data table, we combined "uid" and "action\_id" into the main index. There can only be one set of the main index, so you will never have a chance to have a second set of duplicate data. If you insist on registering, the message "Duplicate entry '2-1' for key 'PRIMARY'" will appear.
2. "Then why amend it?" Because, do you think users can understand the meaning of "Duplicate entry '2-1' for key 'PRIMARY'"? Not to mention that when the user has clearly reported the event, but still sees the "I want to sign up" button on the event page, how will he evaluate the developer at this time?
3. Therefore, please modify one of the following, as well as in the event page, detect, if the user has already registered, the "I want to register" button will not be displayed.
4. Think about it, what are the methods?

#### 1. Suggested Practice

1. When connected to this module, all the data that the user has participated in will be retrieved, saved as an array, and put into the session
2. When listing activities, just use in\_array\(\) to determine whether the activities are in the array.
3. Advantages, only one more SQL request can be done.

#### Two, modify interface\_menu.php

1.  interface\_menu.php will definitely move when reading the module, so after judging that there is $xoopsUser in it, you can retrieve all the activity numbers that the user has registered

   ```text
   if ($xoopsUser) {
       $module_id = $xoopsModule->getVar('mid');
       $isAdmin   = $xoopsUser->isAdmin($module_id);

       //抓取該使用者已報名的活動編號
       if (!isset($_SESSION['uid_signup'])) {
           $tbl                    = $xoopsDB->prefix('signups');
           $uid                    = $xoopsUser->uid();
           $sql                    = "SELECT action_id FROM `{$tbl}` where `uid`='{$uid}'";
           $result                 = $xoopsDB->query($sql) or web_error($sql);
           $_SESSION['uid_signup'] = [];
           while (list($action_id) = $xoopsDB->fetchRow($result)) {
               $_SESSION['uid_signup'][] = $action_id;
           }
       }
   }
   ```

2. We put all event numbers into the $\_SESSION\['uid\_signup'\] array
3. Since the loop only captured one field, use $xoopsDB-&gt;fetchRow\($result\) instead to capture, and use list\(\) for assignment, and put the value in $action\_id.

#### 3. Modify the signup\(\) registration function

1. ,This part is easy to be ignored. This means that after logging in, if you go to sign up for other activities, it is reasonable to add the activity to the $\_SESSION\['uid\_signup'\] array at the moment of registration.

   ```text
   //報名
   function signup($action_id)
   {
       global $xoopsDB, $xoopsUser;

       $uid = $xoopsUser->uid();

       $tbl = $xoopsDB->prefix('signups');
       $sql = "INSERT INTO `{$tbl}` ( `action_id`, `uid`, `signup_date`)
       VALUES ('{$action_id}', '{$uid}', NOW())";
       $xoopsDB->queryF($sql) or web_error($sql);
       $_SESSION['uid_signup'][] = $action_id;
   }
   ```

#### Fourth, modify the activity list of the main template

1. We can judge directly in the template, edit list\_action.tpl

   ```text
   <{if $xoops_isadmin}>
     <a href="javascript:delete_action(<{$action.action_id}>)" class="btn btn-danger btn-xs">刪除</a>
     <a href="admin/main.php?action_id=<{$action.action_id}>" class="btn btn-warning btn-xs">編輯</a>
   <{elseif $xoops_isuser}>
     <{if $action.action_id|in_array:$smarty.session.uid_signup}>
       <a href="index.php?op=delete_signup&action_id=<{$action.action_id}>" class="btn btn-danger btn-xs">取消報名</a>
     <{else}>
       <a href="index.php?op=signup&action_id=<{$action.action_id}>" class="btn btn-success btn-xs">我要報名</a>
     <{/if}>
   <{/if}>
   ```

2. We use smarty's variable modifier and directly use PHP's in\_array\(\) function to determine whether the current activity number is in the $\_SESSION\['uid\_signup'\] array

