# 6-3 Read single data from database



#### 1. Read data from the database

1. To read the contents of the database, always use the select syntax:

   ```text
   SELECT `Query field` [FROM `Table name` additional filter conditions]
   ```

2. The filter condition syntax is as follows:

   ```text
   [where filter condition]
   [group by `column name`][having group filter condition]
   [order by {unsigned_integer | `Field name` | formula} [asc | desc] ,...]
   [limit [starting point,] number of transactions]
   ```

3. There is a sequence relationship, so pay attention.

#### 2. Get a single content

1. The method of displaying a single content is as follows:

   ```text
   //Show single event
   function show_action($action_id)
   {
       global $xoopsDB, $xoopsTpl;
       $tbl    = $xoopsDB->prefix('actions');
       $sql    = "SELECT * FROM `{$tbl}` WHERE `action_id` ='{$action_id}'";
       $result = $xoopsDB->query($sql) or web_error($sql);
       $action = $xoopsDB->fetchArray($result);
       $xoopsTpl->assign('action', $action);
   }
   ```

2. The $xoopsDB and $xoopsTpl objects are used in the function, so the global declaration must be made first.
3. Write the select read grammar of SQL, specify to read a certain piece of data.
4. Use $xoopsDB-&gt;query to send data, and store the returned controller in a variable, such as $result.
5. Then use $xoopsDB-&gt;fetchArray\($result\) to get the data array. Among them, the array content of $action is similar to this:
   * $action\['action\_id'\]=1;
   * $action\['title'\]='The absolute heat of the mountain bay';
   * $action\['content'\]='xxxxxx main content';
   * $action\['action\_date'\]=' 2017-09-02';
   * $action\['end\_date'\]=' 2017-08-31 17:30:00';
   * $action\['uid'\]='1';
   * $action\['enable'\]='1';

