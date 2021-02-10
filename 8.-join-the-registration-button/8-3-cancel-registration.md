# 8-3 Cancel registration

1. Canceling registration is actually deleting a piece of registration information in signups.
2. Remember before teaching [deleted after confirming](https://campus-xoops.tn.edu.tw/modules/tad_book3/page.php?tbdsn=891) it? Just draw the gourd as you like!

#### 1. Modify the link and generate related functions

1. Also change the cancellation link to this:

   ```text
   <a href="javascript:delete_signup({$action.action_id})" class="btn btn-danger btn-xs">取消報名</a>
   ```

2. Then modify the list\_action function of index.php to use the built-in sweet\_alert category of tadtools to generate a set of deleted js functions to make the "delete function after confirmation":

   ```text
   //顯示活動列表
   function list_action()
   {
       global $xoopsDB, $xoopsTpl, $isAdmin;

       $tbl   = $xoopsDB->prefix('actions');
       $where = $isAdmin ? '' : "WHERE `enable` ='1' AND `end_date` > now() ";
       $sql   = "SELECT * FROM `{$tbl}` $where ORDER BY `end_date` DESC";

       //getPageBar($原sql語法, 每頁顯示幾筆資料, 最多顯示幾個頁數選項);
       $PageBar = getPageBar($sql, 5, 10);
       $bar     = $PageBar['bar'];
       $sql     = $PageBar['sql'];
       $total   = $PageBar['total'];
       $xoopsTpl->assign('bar', $bar);
       $xoopsTpl->assign('total', $total);

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
       $sweet_alert2 = new sweet_alert();
       $sweet_alert2->render("delete_signup", "index.php?op=delete_signup&action_id=", 'action_id', "確定要取消嗎？" , "取消後就不能參加活動囉！" , "是！含淚取消！");
   }
   ```

#### Two, make the delete function

1. Then go to index.php, first add a set of processes:

   ```text
   case "delete_signup":
       delete_signup($action_id);
       header("location:{$_SERVER['PHP_SELF']}?action_id=$action_id");
       exit;
   ```

2. Then actually make the function:

   ```text
   //取消報名
   function delete_signup($action_id)
   {
       global $xoopsDB, $xoopsUser;

       $uid = $xoopsUser->uid();

       $tbl = $xoopsDB->prefix('signups');
       $sql = "DELETE FROM `{$tbl}` WHERE `action_id`='{$action_id}' and `uid`='{$uid}'";
       $xoopsDB->queryF($sql) or web_error($sql);
       $_SESSION['uid_signup'] = array_diff($_SESSION['uid_signup'], [$action_id]);
   }
   ```

3. If you sign up, you need to add the activity to the $\_SESSION\['uid\_signup'\] array. Similarly, if you cancel the registration, you must remove the number from the $\_SESSION\['uid\_signup'\] array. What happens if you don't take it away? Nothing. The system did delete the data, but the "Cancel Registration" button will still appear for the event.
4. Therefore, we use [array\_diff\(\[array one\], \[array two\]\)](http://php.net/manual/en/function.array-diff.php) to delete a value in the array.

#### Three, about array\_diff\(\)

1. This is actually not a function to remove the contents of the array, but to compare the difference between the two arrays and return the difference to a new array.
2. So, assuming that there are three activities in the $\_SESSION\['uid\_signup'\] array, in order \[1, 2, 3\], then, if you want to cancel activity 2, we only need to write array\_diff\(\[1, 2, 3\], \[2 \]\), the function will return the array \[1, 3\], because this is just the difference, does it look like 2 has been deleted!

