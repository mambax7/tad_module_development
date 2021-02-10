# 8-1 Join the registration function

#### 1. Joining process

1. Since the button is linked to index.php, its op is signup, so follow the old method to build a process and make a function.
2. Modify the process and add a group:

   ```text
   case "signup":
       signup($action_id);
       header("location:{$_SERVER['PHP_SELF']}?action_id=$action_id");
       exit;
   ```

3. After signing up, go directly to the event, we hope to see the list of already registered under the event

#### 2. Make registration function

1. Add the signup\(\) function in index.php, and add the registration information to signups

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
   }
   /*--
   ```

