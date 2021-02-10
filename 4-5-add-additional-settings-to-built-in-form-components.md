# 4-5 Add additional settings to built-in form components

 Using the [$ form element -&gt; setExtra\(\)](http://api.xoops.org/2.5.9/class-XoopsFormElement.html#_setExtra) method, you can add any additional syntax to the form element, for example:

```text
$Text->setExtra("class='form-control'");
$Text->setExtra("style='width: 90%'");
$Text->setExtra("placeholder='請輸入標題'");
```

