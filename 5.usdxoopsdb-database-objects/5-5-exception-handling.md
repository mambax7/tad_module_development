# 5-5 Exception handling



1. Since there is an error in the data filtering check, an exception will be thrown, so we must accept it.
2. We wrap the entire switch, and have received the exception thrown when executing the action

   ```text
   try
   {
       switch ($op) {

           case "insert_action":
               $action_id = insert_action();
               header("location:{$_SERVER['PHP_SELF']}?action_id={$action_id}");
               exit;

           default:
               action_form();
               break;
       }
   } catch (exception $e) {
       $xoopsTpl->assign('error', $e->getMessage());
   }
   ```

3. We threw the exception message received by the street to the template and applied it to the template variable &lt;{$error}&gt;.
4. So let's make a simple error presentation template templates/error\_alert.tpl

   ```text
   <{if $error}>
     <div class="alert alert-danger">
       <{$error}>
     </div>
   <{/if}>
   ```

5. If you don't want to register the template in xoops\_version.php, we can use the includeq syntax to import the template file:

   ```text
   <{includeq file="$xoops_rootpath/modules/模組名稱/templates/樣板.tpl"}>
   ```

6. Edit the existing template templates/tad\_signup\_adm\_main.tpl to import it

   ```text
   <div class="container-fluid">
     <{includeq file="$xoops_rootpath/modules/tad_signup/templates/error_alert.tpl"}>
     <{$action_form}>
   </div>
   ```

7. If it is troublesome, it is also a good way to turn directly:

   ```text
   } catch (exception $e) {
       redirect_header($_SERVER['PHP_SELF'], 3, $e->getMessage());
   }
   ```

8. Or use the built-in error message box

   ```text
   } catch (exception $e) {    
       xoops_error($e->getMessage(), '錯誤訊息');
   }
   ```

