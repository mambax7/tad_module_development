# 4-9 Complete form function



1. The final full version looks like this:

   ```text
   //顯示預設頁面內容
   function action_form()
   {

       global $xoopsTpl;

       include_once XOOPS_ROOT_PATH . "/class/xoopsformloader.php";
       $val = ['title' => '', 'action_date' => date('Y-m-d'), 'end_date' => date('Y-m-d 17:30:00'), 'enable' => '1', 'content' => ''];

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

       $form->addElement(new XoopsFormHidden('op', 'insert_action'));
       $Tray = new XoopsFormElementTray('', '&nbsp;', 'name');
       $Tray->addElement(new XoopsFormButton('', 'name', '清除', 'reset'));
       $Tray->addElement(new XoopsFormButton('', 'name', '送出', 'submit'));
       $form->addElement($Tray);
       $action_form = $form->render();

       $xoopsTpl->assign('action_form', $action_form);
   }
   ```

2. Once opened, use $val = \[\]; to set the default value.
3. Finally, send the generated form to the template file

