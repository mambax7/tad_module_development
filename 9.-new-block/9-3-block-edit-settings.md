# 9-3 Block edit settings



1. To add the setting function of the area, you can edit the editing function list\_signup\_edit\($options\) in the block file blocks/list\_signup.php:

   ```text
   //區塊編輯函數
   function list_signup_edit($options)
   {
       $opt0_1 = $options[0] == 1 ? 'checked' : '';
       $opt0_0 = $options[0] != 1 ? 'checked' : '';
       $form   = "
       <div class='form-group'>
         <label class='col-sm-2 control-label'>
           是否顯示報名按鈕？
         </label>
         <div class='col-sm-10'>
           <label class='radio-inline'>
             <input type='radio' name='options[0]' value=1 {$opt0_1}> 是
           </label>
           <label class='radio-inline disabled'>
             <input type='radio' name='options[0]' value=0 {$opt0_0}> 否
           </label>
         </div>
       </div>";
       return $form;
   }
   ```

2. We add a block editing interface function to the original block program blocks/list\_signup.php. The purpose is to generate a block setting interface, the name must be consistent with edit\_func.
3. The editing interface function is actually just a web form, but &lt;form&gt;&lt;/form&gt; is not needed.
4. The default value of the form field is the options setting value in xoops\_version.php. The default value is passed and used through the $options array.

