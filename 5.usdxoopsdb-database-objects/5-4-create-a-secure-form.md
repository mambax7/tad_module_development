# 5-4 Create a secure form

When saving or updating, please add the following section to check the syntax. If it is not a valid form, an exception will be thrown:

```text
//安全判斷
if(!$GLOBALS['xoopsSecurity']->check()){
  $error=implode("<br>" , $GLOBALS['xoopsSecurity']->getErrors());
  throw new Exception($error);
}
```

