# 4-6 Modify the calendar component



1. The official calendar picker is actually okay, but the time picker is quite troublesome when receiving processing time, so we can use our favorite calendar picker instead. For example: [http://my97.net/demo/index.htm](http://my97.net/demo/index.htm)
2. Edit the action\_form\(\) function and add the following syntax to it so that XOOPS can automatically load the relevant js files of the monthly calendar

   ```text
   include_once XOOPS_ROOT_PATH . "/modules/tadtools/cal.php";
   $cal = new My97DatePicker();
   $cal->render();
   ```

3. Since WdatePicker needs to add the onClick="WdatePicker\(\)" grammar in the input field of the date to be activated, then you need to modify the original time object and use the text input object XoopsFormText to apply the monthly calendar:

   ```text
   $action_date = new XoopsFormText('活動日期', 'action_date', 15, 255, $val['action_date']);
   $action_date->setExtra("onClick=\"WdatePicker()\"");
   $form->addElement($action_date, true);
   ```

4. The deadline is the same, but because the time is added, the setting item of WdatePicker\(\) will be longer

   ```text
   $end_date = new XoopsFormText('截止日期', 'end_date', 15, 255, $val['end_date']);
   $end_date->setExtra("onClick=\"WdatePicker({dateFmt:'yyyy-MM-dd HH:mm:ss', startDate:'%y-%M-%d 17:30:00'})\"");
   $form->addElement($end_date, true);
   ```

