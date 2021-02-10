# 6-4 Make and display a single event page



1. Since index.php uses the tad\_signup\_index.tpl template, let’s simply edit templates/tad\_signup\_index.tpl

   ```text
   <{if $op=="show_action"}>
     <h2><{$action.title}></h2>
     <div class="panel panel-primary">
         <div class="panel-heading">活動日期：<{$action.action_date}></div>
         <div class="panel-body">
             <{$action.content}>
         </div>
     </div>
   <{/if}>
   ```

2. Check if there is any effect!
3. BootStrap3 panel: [http://v3.bootcss.com/components/\#panels](http://v3.bootcss.com/components/#panels)

