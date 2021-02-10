# 7-2 Update activity

#### 1. SQL syntax for updating data

1. SQL syntax for updating information:

   ```text
   update `資料表名稱` set `欄位1`='值1', `欄位2`='值2', ... [where 篩選條件] [limit 筆數]
   ```

#### 2. Add the update function

1. Since $op will become update\_action when modified, it is necessary to do a set of process corresponding to this $op, modify admin/main.php, and edit the process:

   ```text
   case "update_action":
       update_action();
       header("location: ../index.php?action_id={$action_id}");
       exit;
   ```

2. Then, actually make the update\_action\(\) function.

   ```text
   //更新資料庫
   function update_action()
   {
       global $xoopsDB, $xoopsUser;
       //安全判斷
       if (!$GLOBALS['xoopsSecurity']->check()) {
           $error = implode("<br>", $GLOBALS['xoopsSecurity']->getErrors());
           throw new Exception($error);
       }

       $action_id   = clean_var('action_id', '活動編號');
       $title       = clean_var('title', '活動名稱');
       $action_date = clean_var('action_date', '活動日期');
       $end_date    = clean_var('end_date', '截止日期');
       $enable      = clean_var('enable', '使否啟用');
       $content     = clean_var('content', '活動內容');
       $uid         = $xoopsUser->uid();

       $sql = "UPDATE `" . $xoopsDB->prefix('actions') . "` SET
       `title`='{$title}',
       `content`='{$content}',
       `action_date`='{$action_date}',
       `end_date`='{$end_date}',
       `uid`='{$uid}',
       `enable`='{$enable}'
       WHERE `action_id`= '$action_id'";
       $xoopsDB->query($sql) or web_error($sql);
   }
   ```

