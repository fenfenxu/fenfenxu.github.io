---     
  layout: post
  title: Remote webview inspector
---

#### weinre

weinre， 可以远程连接手机的webview页面，进行查看广告页面里的dom结构
此方法区别于手机chrome的远程调试功能， 此可以应用到自定义的webview中

#### 安装： (需要 node + npm ):

        $sudo npm -g install weinre

#### 使用：

+ 启动weinre server:  

    $ weinre --httpPort 8088 --boundHost 192.168.3.32 //(我本机ip)

+ 然后需要向需要inspect的webview中注入如下js代码：

        webview.loadUrl("javascript:(function(e){e.setAttribute('src','http://192.168.3.32:8088/target/target-script-min.js#anonymous');document.getElementsByTagName('body')[0].appendChild(e);})(document.createElement('script'));void(0);");

+ webview load 成功后即可在 http://192.168.3.32:8088/client/#anonymous中 查看了。