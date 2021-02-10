# 3-2 Background management page main.php



1. Generally speaking, admin/index.php is the home page of the module backend, and admin/main.php is the name of the main operation page of the module backend, but in fact, there is no mandatory requirement.
2. The basic structure is as follows \(the focus is only on the first few lines and the bottom line, the middle part can be written as you please\):

   ```text
   <?php
   /*-----------引入檔案區--------------*/
   $xoopsOption['template_main'] = "樣板檔.tpl";
   include_once "header.php";
   include_once "../function.php";

   /*-----------function區--------------*/

   //顯示預設頁面內容
   function show_content()
   {
       global $xoopsTpl;

       $main = "後台頁面開發中";
       $xoopsTpl->assign('content', $main);
   }

   /*-----------執行動作判斷區----------*/
   include_once $GLOBALS['xoops']->path('/modules/system/include/functions.php');
   $op = system_CleanVars($_REQUEST, 'op', '', 'string');
   // $sn = system_CleanVars($_REQUEST, 'sn', 0, 'int');

   switch ($op) {

       // case "xxx":
       // xxx();
       // header("location:{$_SERVER['PHP_SELF']}");
       // exit;

       default:
           show_content();
           break;
   }

   include_once 'footer.php';
   ```

