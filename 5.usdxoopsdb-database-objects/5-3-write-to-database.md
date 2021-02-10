# 5-3 Write to database



#### One, MySQL insert syntax

1. The SQL syntax for adding data is as follows:

   ```text
   insert [into] 資料表名稱 [(欄位1,欄位2...)] values (值1,值2...)
   ```

2. The brackets can be omitted.

#### 2. Add storage mechanism

1. Since there is a hidden op=insert\_action, first set an additional set of corresponding settings in switch

   ```text
   case "insert_action":
       $action_id = insert_action();
       header("location: ../index.php?action_id={$action_id}");
       exit;
   ```

2. Set to execute the insert\_action\(\) function, which is to add an activity to the database, and hope it can return the activity number so that after saving, you can directly connect to the front-end module home page index.php to watch the activity details.
3. When making the insert\_action\(\) function, the variable when writing must be processed for special symbols \(try to save as much as possible\)

   ```text
   $title       = clean_var('title', '活動名稱');
   $action_date = clean_var('action_date', '活動日期');
   $end_date    = clean_var('end_date', '截止日期');
   $enable      = clean_var('enable', '使否啟用');
   $content     = clean_var('content', '活動內容');
   ```

4. When writing SQL syntax, the table name needs to be prefixed with $xoopsDB-&gt;prefix\('data table'\)

   ```text
   $sql = "INSERT INTO `" . $xoopsDB->prefix('actions') . "`
   ( `title`, `content`, `action_date`, `end_date`, `uid`, `enable`)
   VALUES ('{$title}', '{$content}', '{$action_date}', '{$end_date}', '{$uid}', '{$enable}')";
   $xoopsDB->query($sql) or web_error($sql);
   $action_id = $xoopsDB->getInsertId();
   ```

5. $xoopsDB-&gt;query\($sql\) can be used to send a request
6. web\_error\($sql\); is a function used to display errors when accessing the database, built in the tadtools module
7. $xoopsDB-&gt;getInsertId\(\); used to get the ID of the newly added data

