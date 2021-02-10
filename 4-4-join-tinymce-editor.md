# 4-4 Join TinyMCE editor



1. In terms of WYSIWYG editor, XOOPS only built-in TinyMCE editor
2. The method of use is as follows:

   ```text
   include_once XOOPS_ROOT_PATH . "/class/xoopseditor/xoopseditor.php";
   include_once XOOPS_ROOT_PATH . "/class/xoopseditor/tinymce/formtinymce.php";
   $options['caption'] = "活動內容";
   $options['name']    = 'content';
   $options['value']   = $content;
   $options['width']   = '100%';
   $options['height']  = '400px';
   $form->addElement(new XoopsFormTinymce($options));
   ```

