# 4-3 Various XOOPS form components



1. Basic form components:

   ```text
   //標籤元件
   $Label =new XoopsFormLabel('標題', '內容');
   //文字輸入
   $Text=new XoopsFormText('標題', 'name', 大小 , 最大長度 , '值');
   //隱藏欄位
   $Hidden =new XoopsFormHidden('name', '值');
   //安全檢查
   $Token =new XoopsFormHiddenToken('XOOPS_TOKEN',360);
   //上傳欄位
   $form->setExtra("enctype='multipart/form-data'");
   $File =new XoopsFormFile('標題', 'name', '2048');
   //密碼欄位
   $Password=new XoopsFormPassword('標題', 'name', 大小, 最大長度, '值');
   //大量文字
   $TextArea=new XoopsFormTextArea('標題', 'name', '值' , 欄寬 , 列高 , 'id');
   //文字日期
   $DateSelect=new XoopsFormTextDateSelect('標題', 'name', 大小, '值');
   //日期時間
   $DateTime=new XoopsFormDateTime('標題', 'name', 大小, '值');
   //XOOPS編輯器
   $DhtmlTextArea=new XoopsFormDhtmlTextArea('標題' , 'name',  '值' , 欄寬 , 列高);
   //按鈕
   $Button =new XoopsFormButton('標題', 'name', '值', '類型');
   ```

2. For form components with options, the default value setting method for options is:

   ```text
   $表單元件->setValue($多重預設值陣列);
   ```

3. There are two ways to add options, the first is to add one by one:

   ```text
   $表單元件->addOption('選單值1', '顯示值1', false);
   ```

4. The second is to set up the option array first and add it all at once. \(And the above method can be used at the same time\)

   ```text
   $options['選單值2']='顯示值2';
   $options['選單值3']='顯示值3';
   $表單元件->addOptionArray($options);
   ```

5. All form components with options:

   ```text
   //複選方塊
   $CheckBox = new XoopsFormCheckBox('標題', 'name', '值','id');
   //單選鈕
   $Radio = new XoopsFormRadio('標題', 'name', '值');
   //是否單選
   $RadioYN=new XoopsFormRadioYN('標題', 'name', '值');
   //下拉選單
   $Select=new XoopsFormSelect('標題', 'name', '預設值', 大小, 多選);
   //群組核選
   $SelectCheckGroup=new XoopsFormSelectCheckGroup('標題', 'name', '值', 大小 ,多選);
   //國家選單
   $SelectCountry=new XoopsFormSelectCountry('標題', 'name', 'TW', 大小);
   //編輯器選單
   $SelectEditor=new XoopsFormSelectEditor(&$form, 'name', '值', 使用HTML , 可選編輯器陣列);
   //群組選單
   $SelectGroup=new XoopsFormSelectGroup('標題', 'name', 含訪客, '值', 大小 ,多選);
   //語系選單
   $SelectLang=new XoopsFormSelectLang('標題', 'name', '值', 大小);
   //比對選單
   $SelectMatchOption=new XoopsFormSelectMatchOption('標題', 'name', '值', 大小);
   //佈景選單
   $SelectTheme=new XoopsFormSelectTheme('標題', 'name', '值', 大小);
   //時區選單
   $SelectTimezone=new XoopsFormSelectTimezone('標題', 'name', '值', 大小);
   //使用者選單
   $SelectUser=new XoopsFormSelectUser('標題', 'name', 含訪客, '值', 大小 ,多選);
   ```

