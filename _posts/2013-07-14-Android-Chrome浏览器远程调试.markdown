---     
  layout: post
  title: Android Chrome浏览器远程调试
---
{{ page.title }}
===================

[官方文档](https://developers.google.com/chrome-developer-tools/docs/remote-debugging?hl=zh-CN)

### steps

    1 打开移动端版本的Chrome：设置——开发者工具——勾选启用USB网页调试，然后随便打开一个网页。

    2 adb forward tcp:9222 localabstract:chrome_devtools_remote
    访问：http://localhost:9222

### problems

    1 改host:
        203.208.46.178 chrome-devtools-frontend.appspot.com

    2 访问 http://localhost:9222/json 获得所有tab的json数据，看到webSocketDebuggerUrl这一项，copy出来，大致是ws://localhost:9222/devtools/page/1。这个是websocket协议。
    然后，通过chrome-devtools://devtools/devtools.html?docked=true&toolbarColor=rgba(223,223,223,1)&textColor=rgba(0,0,0,1)&ws=localhost:9222/devtools/page/1 访问即可。
    [ws=]部分替换成相应的page就可以了。

<div id="SOHUCS"></div>
<script>
  (function(){
    var appid = 'cyqNyyPhB',
    conf = 'prod_505259756244493872b7709a8a01b536';
    var doc = document,
    s = doc.createElement('script'),
    h = doc.getElementsByTagName('head')[0] || doc.head || doc.documentElement;
    s.type = 'text/javascript';
    s.charset = 'utf-8';
    s.src =  'http://assets.changyan.sohu.com/upload/changyan.js?conf='+ conf +'&appid=' + appid;
    h.insertBefore(s,h.firstChild);
    window.SCS_NO_IFRAME = true;
  })()
</script>     
