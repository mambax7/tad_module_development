# 4-2 Send the data to the template for presentation



#### 1. About XOOPS model engine

1. XOOPS’s template engine uses smarty 2.6.x \(so, the new smarty 3.x syntax cannot be used\)
2. The sample engine object is $xoopsTpl
3. The syntax for applying variables to the template is

   ```text
   $xoopsTpl->assign('樣板變數名稱' , $PHP變數);
   ```

4. In the template, the variables are presented in the following ways:

   ```text
   <{$樣板變數名稱}>
   ```

#### 2. Output the form to the screen

1. Simply organize the architecture:

   ```text
   //顯示預設頁面內容
   function action_form()
   {
       global $xoopsTpl;

       include_once XOOPS_ROOT_PATH . "/class/xoopsformloader.php";
       $val = ['title' => '', 'action_date' => date('Y-m-d'), 'end_date' => date('Y-m-d 17:30:00'), 'enable' => '1', 'content' => ''];

       $form = new XoopsThemeForm('編輯活動', 'name', 'main.php', 'post', true);
       //各種表單元件
       $action_form = $form->render();

       $xoopsTpl->assign('action_form', $action_form);
   }
   ```

2. Finally, insert the template file in templates/tad\_signup\_adm\_main.tpl:

   ```text
   <div class="container-fluid">
     <{$action_form}>
   </div>
   ```

