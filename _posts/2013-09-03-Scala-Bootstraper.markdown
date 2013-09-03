---     
  layout: post
  title: Scala-Bootstraper
---
{{ page.title }}
===================
　
    twitter的scala-bootstraper是用来生成基于sbt构建的项目骨架的工具(gem)
---------------------------

### 使用中有一些问题：

1 首先，项目里project/plugins.sbt里依赖配置的 resolvers: 


    "twitter.com" at "http://maven.twttr.com/"  //此地址不通
    ---->
     "typesafe" at "http://typesafe.artifactoryonline.com/typesafe/twitter"


     "local" at ("file:" + System.getProperty("user.home") + "/.m2/repo/"         
    ----->
     "local" at ("file:" + System.getProperty("user.home") + "/.m2/repository/"     //我机器的maven本地库的位置


同样在build.sbt中添加：// 见[plugin: sbt-package-dist](https://github.com/twitter/sbt-package-dist/blob/master/src/main/scala/com/twitter/sbt/DefaultRepos.scala)

     resolvers += "typesafe" at "http://typesafe.artifactoryonline.com/typesafe/twitter"
     resolvers <<= DefaultRepos.defaultResolvers


2 另，插件sbt11-scrooge是用来生成thrift java。其在使用时会先去 “http://maven.twttr.com/” 加载一个文件.

可以设置环境变量：// 见[plugin:sbt-scrooge](https://github.com/twitter/sbt-scrooge/blob/master/src/main/scala/com/twitter/sbt/CompileScrooge.scala)

    SBT_PROXY_REPO=“http://typesafe.artifactoryonline.com/typesafe/twitter”


3 根据以上改动我fork了一个版本：[Forked scala-bootstrapper](https://github.com/fenfenxu/scala-bootstrapper)


{{ page.date | date_to_string }}
