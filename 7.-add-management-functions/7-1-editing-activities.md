# 7-1 Edit event



1. Edit the template first and add the "Edit" button according to the identity

   ```text
   <td>
     <{if $isAdmin}>
       <a href="admin/main.php?action_id=<{$action.action_id}>" class="btn btn-warning btn-xs">編輯</a>
     <{/if}>
     <a href="index.php?action_id=<{$action.action_id}>" class="btn btn-info btn-xs">詳情</a>
   </td>
   ```

2. Then edit admin/main.php and modify its process, because there is a variable passed in action\_id, which means that the content of the data needs to be modified.

   ```text
   /*-----------執行動作判斷區----------*/
   include_once $GLOBALS['xoops']->path('/modules/system/include/functions.php');
   $op        = system_CleanVars($_REQUEST, 'op', '', 'string');
   $action_id = system_CleanVars($_REQUEST, 'action_id', 0, 'int');
   try
   {
       switch ($op) {

           case "insert_action":
               $action_id = insert_action();
               header("location: ../index.php?action_id={$action_id}");
               exit;

           default:
               action_form($action_id);
               break;
       }
   } catch (exception $e) {
       redirect_header($_SERVER['PHP_SELF'], 3, $e->getMessage());
       // $xoopsTpl->assign('error', $e->getMessage());
   }
   include_once 'footer.php';
   ```

3. The most important thing is to modify the original form function and add some more actions to the editing state:

   ```text
   //顯示預設頁面內容
   function action_form($action_id = '')
   {

       global $xoopsTpl, $xoopsDB;

       include_once XOOPS_ROOT_PATH . "/class/xoopsformloader.php";
       if ($action_id) {
           $tbl    = $xoopsDB->prefix('actions');
           $sql    = "SELECT * FROM `{$tbl}` WHERE `action_id` ='{$action_id}'";
           $result = $xoopsDB->query($sql) or web_error($sql);
           $val    = $xoopsDB->fetchArray($result);
           $op     = 'update_action';
       } else {
           $val = ['title' => '', 'action_date' => date('Y-m-d'), 'end_date' => date('Y-m-d 17:30:00'), 'enable' => '1', 'content' => ''];
           $op  = 'insert_action';
       }

       $form = new XoopsThemeForm('編輯活動', 'name', 'main.php', 'post', true);
       $form->addElement(new XoopsFormText('活動名稱', 'title', 40, 255, $val['title']), true);

       include_once XOOPS_ROOT_PATH . "/modules/tadtools/cal.php";
       $cal = new My97DatePicker();
       $cal->render();
       $action_date = new XoopsFormText('活動日期', 'action_date', 15, 255, $val['action_date']);
       $action_date->setExtra("onClick=\"WdatePicker()\"");
       $form->addElement($action_date, true);

       $end_date = new XoopsFormText('截止日期', 'end_date', 15, 255, $val['end_date']);
       $end_date->setExtra("onClick=\"WdatePicker({dateFmt:'yyyy-MM-dd HH:mm:ss', startDate:'%y-%M-%d 17:30:00'})\"");
       $form->addElement($end_date, true);

       $form->addElement(new XoopsFormRadioYN('使否啟用', 'enable', $val['enable']));

       include_once XOOPS_ROOT_PATH . "/modules/tadtools/ck.php";
       $ck = new CKEditor("tad_signup", "content", $val['content']);
       $ck->setHeight(350);
       $editor = $ck->render();
       $form->addElement(new XoopsFormLabel('活動內容', $editor));

       $form->addElement(new XoopsFormHidden('op', $op));
       $form->addElement(new XoopsFormHidden('action_id', $action_id));
       $Tray = new XoopsFormElementTray('', '&nbsp;', 'name');
       $Tray->addElement(new XoopsFormButton('', 'name', '清除', 'reset'));
       $Tray->addElement(new XoopsFormButton('', 'name', '送出', 'submit'));
       $form->addElement($Tray);
       $action_form = $form->render();

       $xoopsTpl->assign('action_form', $action_form);
   }
   ```

