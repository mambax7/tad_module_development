# 7-5 Display different content according to different identities

1. The current activity list shows the activities that Shan selected has started and the deadline has not yet arrived.
2. However, this has a disadvantage, that is, if it has been closed or the deadline has passed, the administrator will never manage it! \(Because it will not appear\)
3. How to solve? Of course, all unfiltered activities can be listed in the background, but this requires a little more work! Therefore, the simplest way is to display different content for different identities.

   ```text
   //顯示活動列表
   function list_action()
   {
       global $xoopsDB, $xoopsTpl, $isAdmin;

       $tbl    = $xoopsDB->prefix('actions');
       $where  = $isAdmin ? '' : "WHERE `enable` ='1' AND `end_date` > now() ";
       $sql    = "SELECT * FROM `{$tbl}` $where ORDER BY `end_date` DESC";
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
   }
   ```

   |  |
   | :--- |

