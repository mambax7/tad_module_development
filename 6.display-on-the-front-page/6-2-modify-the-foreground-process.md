# 6-2 Modify the foreground process

1. We hope that once you enter the module homepage, you will see the list of activities, but if there is an incoming activity number $action\_id, then a single activity will be displayed. Let’s take a look at the filtering of incoming variables \(this is the official usage, common type\) There are string, int, array\):

   ```text
   /*-----------Action Permission area----------*/
   include_once $GLOBALS['xoops']->path('/modules/system/include/functions.php');
   $op        = system_CleanVars($_REQUEST, 'op', '', 'string');
   $action_id = system_CleanVars($_REQUEST, 'action_id', 0, 'int');
   ```

2. The process part is changed to this:

   ```text
   try
   {
       switch ($op) {

           default:
               if ($action_id) {
                   show_action($action_id);
                   $op = "show_action";
               } else {
                   list_action();
                   $op = "list_action";
               }
               break;
       }
   } catch (exception $e) {
       redirect_header($_SERVER['PHP_SELF'], 3, $e->getMessage());
   }

   /*-----------Show result area--------------*/
   $xoopsTpl->assign('op', $op);
   include_once XOOPS_ROOT_PATH . '/footer.php';
   ```

3. Since there is no `$op` in default \(used to tell the program what to do now\), we define a $op value by ourselves. The purpose is to also pass the current action to the template, so that the template can also be based on `$op` Different, present different content.
4. Next, we reserve two empty functions to avoid execution errors.

   ```text
   //Show a single event
   function show_action($action_id)
   {
       global $xoopsTpl;

       $main = "";
       $xoopsTpl->assign('content', $main);
   }

   //Display the list of activities
   function list_action()
   {
       global $xoopsTpl;

       $main = "";
       $xoopsTpl->assign('content', $main);
   }
   ```

