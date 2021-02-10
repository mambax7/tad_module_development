# 4-1 Basic usage of XOOPS form objects



1. Starting from 2.5.9, form objects can support BootStrap3!
2. To use the built-in form, you need to introduce this line:

   ```text
   include_once(XOOPS_ROOT_PATH."/class/xoopsformloader.php");
   ```

3. Create a form \( [http://api.xoops.org/2.5.9/class-XoopsThemeForm.html](http://api.xoops.org/2.5.9/class-XoopsThemeForm.html) \):

   ```text
   $form = new XoopsThemeForm('表單標題', 'name', 'main.php', 'post', '使用token' , '摘要');

   ```

4. How to add form elements to the form \( [http://api.xoops.org/2.5.9/class-XoopsForm.html\#\_addElement](http://api.xoops.org/2.5.9/class-XoopsForm.html#_addElement) \):

   ```text
   $form->addElement($元件變數, $是否必填);
   ```

5. To make the field mandatory, you must set the name in new XoopsThemeForm\(\) when creating the form, and set the second parameter to true when adding elements in addElement\(\).
6. Combine several elements together and put them in the form \( [http://api.xoops.org/2.5.9/class-XoopsFormElementTray.html](http://api.xoops.org/2.5.9/class-XoopsFormElementTray.html) \):

   ```text
   $Tray=new XoopsFormElementTray('標題', '&nbsp;', 'name');
   $Tray->addElement(new XoopsFormButton('', 'name', '送出', 'submit'));
   $Tray->addElement(new XoopsFormButton('', 'name', '清除', 'reset'));
   $form->addElement($Tray);
   ```

7. Generate form code and return:

   ```text
   $f=$form->render();
   ```

  
  

