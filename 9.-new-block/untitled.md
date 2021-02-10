# 10. Join search

1. First go to the background block management and enable XOOPS search block.
2. Add search settings in xoops\_version.php \(remember to update the module\):

   ```text
   //---搜尋---//
   $modversion['hasSearch']      = 1;
   $modversion['search']['file'] = "include/search.php";
   $modversion['search']['func'] = "tad_signup_search";
   ```

3. Edit include/search.php and modify it according to the prompts.

   ```text
   <?php
   function tad_signup_search($queryarray, $andor, $limit, $offset, $userid)
   {
       global $xoopsDB;
       if (get_magic_quotes_gpc()) {
           foreach ($queryarray as $k => $v) {
               $arr[$k] = addslashes($v);
           }
           $queryarray = $arr;
       }
       $sql = "SELECT `action_id`,`title`,`action_date`, `uid` FROM " . $xoopsDB->prefix("actions") . " WHERE `enable`=1";
       if ($userid != 0) {
           $sql .= " AND uid=" . $userid . " ";
       }
       if (is_array($queryarray) && $count = count($queryarray)) {
           $sql .= " AND ((`title` LIKE '%{$queryarray[0]}%'  OR `content` LIKE '%{$queryarray[0]}%' )";
           for ($i = 1; $i < $count; $i++) {
               $sql .= " $andor ";
               $sql .= "(`title` LIKE '%{$queryarray[$i]}%' OR  `content` LIKE '%{$queryarray[$i]}%' )";
           }
           $sql .= ") ";
       }
       $sql .= "ORDER BY  `action_date` DESC";
       $result = $xoopsDB->query($sql, $limit, $offset);
       $ret    = array();
       $i      = 0;
       while ($myrow = $xoopsDB->fetchArray($result)) {
           $ret[$i]['image'] = "images/search.png";
           $ret[$i]['link']  = "index.php?action_id=" . $myrow['action_id'];
           $ret[$i]['title'] = $myrow['title'];
           $ret[$i]['time']  = strtotime($myrow['action_date']);
           $ret[$i]['uid']   = $myrow['uid'];
           $i++;
       }
       return $ret;
   }
   ```

4. For the icon ![](https://campus-xoops.tn.edu.tw/uploads/tad_book3/image/29/search.png), please prepare a 16x16 icon and save it as images/search.png. \(Can be downloaded from [https://www.flaticon.com](https://www.flaticon.com/) \)

