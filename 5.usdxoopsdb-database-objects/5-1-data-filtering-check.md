# 5-1 Data filtering check

1. When writing, the text must be processed for special symbols \(try to save as much as possible\)
   * [https://www.thenewslens.com/article/74761](https://www.thenewslens.com/article/74761)
   * [http://www.appledaily.com.tw/realtimenews/article/new/20151113/731514/](http://www.appledaily.com.tw/realtimenews/article/new/20151113/731514/)
2. When depositing, if there are special symbols, such as: "\", """, "'", if it is not processed, it may not be possible to deposit. We use the built-in [MyTextSanitizer](http://api.xoops.org/2.5.9/class-MyTextSanitizer.html) text filtering tool to process

   ```text
   $myts = MyTextSanitizer::getInstance();
   ```

3. It is very common to add escape slashes for special symbols to smoothly store them in the database.

   ```text
   $myts->addSlashes(文字);
   ```

4. Used to filter indecent characters, it needs to be used with the "Preferences→System Settings→Sensitive Word Check" setting in the XOOPS background.

   ```text
   $myts->censorString(文字);
   ```

5. We make it into a clean\_var\(\) function and put it in function.php so that both the front and back ends can be called and used

   ```text
   //檢查並傳回欲拿到資料使用的變數
   function clean_var($var = '', $title = '', $filter = '')
   {
       $myts = MyTextSanitizer::getInstance();
       $var  = $myts->addSlashes($_REQUEST[$var]);

       if (empty($var)) {
           throw new Exception("{$title}為必填！");
       } 

       if ($filter) {
           $var = filter_var($var, $filter);
           if (!$var) {
               throw new Exception("不合法的{$title}");
           }
       }
       return $var;
   }
   ```

