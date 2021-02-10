# 4-7 Switch to CKEditor editor



1. It's not that TinyMCE is not easy to use, but the CKEditor we have modified by ourselves is more sophisticated and powerful, so you can try changing the editor to CKEditor
2. Mr. CKEditor built in tadtools.

   ```text
   include_once XOOPS_ROOT_PATH . "/modules/tadtools/ck.php";
   $ck = new CKEditor("tad_signup", "content", $val['content']);
   $ck->setHeight(350);
   $editor = $ck->render();
   ```

3. Then, use XoopsFormLabel\(\) to stuff any content into the form.

   ```text
   $form->addElement(new XoopsFormLabel('活動內容', $editor));
   ```

