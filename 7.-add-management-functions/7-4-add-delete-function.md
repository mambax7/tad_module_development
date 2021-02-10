# 7-4 Add delete function

#### 1. SQL syntax for deleting data

1. The deleted SQL syntax is as follows:

   ```text
   delete from `資料表名稱` [where 篩選條件] [limit 筆數]
   ```

#### 2. Add delete function

1. Modify admin/main.php and add a set of deleted processes:

   ```text
   case "delete_action":
       delete_action($action_id);
       header("location: ../index.php");
       exit;
   ```

2. Then, actually make the delete\_action\(\) function.

   ```text
   //刪除活動
   function delete_action($action_id)
   {
       global $xoopsDB;

       $sql = "DELETE FROM `" . $xoopsDB->prefix('actions') . "` WHERE `action_id`='{$action_id}'";
       $xoopsDB->queryF($sql) or web_error($sql);
   }
   ```

