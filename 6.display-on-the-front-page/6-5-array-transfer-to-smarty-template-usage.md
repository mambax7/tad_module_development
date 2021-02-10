# 6-5 Array transfer to Smarty template usage



### 6-5 How to transfer array to Smarty template

| Transfer content | PHP file \(\*.php\) | Smarty template file \(\*.tpl\) |
| :--- | :--- | :--- |
| General variables |  |  |
| One-dimensional array |  |  |
| Two-dimensional array |  |  |

#### Smarty loop related usage in XOOPS

1. Smarty loops are used to process arrays. Common methods are as follows:

   ```text
   <{foreach from=$來源變數 item=$別名 name=迴圈別名}>
     <{$別名.索引}>
   <{foreachelse}>
     該變數沒有值時要出現的內容
   <{/foreach}>
   ```

2. There are also some special uses for loops:
   * &lt;{$smarty.foreach.loop alias.first}&gt; The first loop of the loop
   * &lt;{$smarty.foreach.loop alias.last}&gt; the last lap of the loop
   * &lt;{$smarty.foreach.loop alias.index}&gt; Get the index value of the loop, and output 0, 1, 2...
   * &lt;{$smarty.foreach.loop alias.iteration}&gt; Get the count value of the loop, and output 1, 2, 3...
   * &lt;{$smarty.foreach.loop alias.total}&gt; Get the total number of loop executions
3. For details, please see: [https://www.smarty.net/docsv2/en/language.function.foreach.tpl](https://www.smarty.net/docsv2/en/language.function.foreach.tpl)

