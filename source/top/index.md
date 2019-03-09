
---
title: Top5
comments: false
keywords: top,文章阅读量排行榜
date: 2017-09-18 05:28:57
---
<div id="top"></div>
<script src="https://cdn1.lncld.net/static/js/av-core-mini-0.6.4.js"></script>
<script>AV.initialize("app_id", "app_key");</script>
<script type="text/javascript">
  var time=0
  var title=""
  var url=""
  var query = new AV.Query('Counter');
  query.notEqualTo('id',0);
  query.descending('time');
  query.limit(5);
  query.find().then(function (todo) {
    for (var i=0;i<5;i++){ 
      var result=todo[i].attributes;
      time=result.time;
      title=result.title;
      url=result.url;
      var content="<a href='"+"https://reuixiy.github.io"+url+"'>"+title+"</font>"+"</a>"+"<br>"+"<font color='#000'>"+"阅读次数："+time+"<br><br>";
      document.getElementById("top").innerHTML+=content
    }
  }, function (error) {
    console.log("error");
  });
</script>

