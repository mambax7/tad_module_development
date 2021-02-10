# 5-2 $xoopsUser user object to obtain user data



1. 2. The [$xoopsUser object](http://api.xoops.org/2.5.9/class-XoopsUser.html) will only [appear](http://api.xoops.org/2.5.9/class-XoopsUser.html) after the user logs in . If there is no such object, it means that they have not logged in.
3. To use in functions, remember:

   ```text
   global $xoopsUser;
   ```

4. Several commonly used $xoopsUser object methods:
   * Get user ID

     ```text
     $uid = $xoopsUser->uid();
     ```

   * Get the user's real name

     ```text
     $name = $xoopsUser->name();
     ```

   * Get user login account

     ```text
     $uname= $xoopsUser->uname();
     ```

   * Get user email

     ```text
     $email= $xoopsUser->email();
     ```

   * Get user's personal website

     ```text
     $url= $xoopsUser->url();
     ```

   * Get user avatar \(avatars/cavt50877193c9788.png\)

     ```text
     $user_avatar= $xoopsUser->user_avatar();
     ```
5. Avoid errors caused by not logging in:

   ```text
   $uid = ($xoopsUser)?$xoopsUser->uid():0;
   ```

6. Get user name by uid

   ```text
   $uid_name = XoopsUser::getUnameFromId($uid,1);
   if(empty($uid_name))$uid_name=XoopsUser::getUnameFromId($uid,0);
   ```

