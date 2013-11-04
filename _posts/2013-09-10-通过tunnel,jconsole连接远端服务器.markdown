---     
  layout: post
  title: 通过tunnel，jconsole连接远端服务器
---


### 通过tunnel，jconsole连接远端服务器

#### 1） 远端java进程启动需要添加：

    JAVA_OPTS="$JAVA_OPTS -Djava.rmi.server.hostname=10.21.125.11 -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=8999 -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false"
    // 为简便禁用掉了验证，不需要用户名密码，ssh key


#### 2 ）本地小脚本：

    function jc {

        host=$1

        proxy_port=${2:-8123}

        jconsole_host=liuxu-desktop

        ssh -f -D$proxy_port $host 'while true; do sleep 1; done'

        ssh_pid=`ps ax | grep "[s]sh -f -D$proxy_port" | awk '{print $1}'`

        jconsole -J-DsocksProxyHost=localhost -J-DsocksProxyPort=$proxy_port service:jmx:rmi:///jndi/rmi://${jconsole_host}:8999/jmxrmi

        kill $ssh_pid

    }

3 ）启动jconsole并连接到远端进程
jc remoteip


需要注意的是：
jconsole_host 需要设置的是 执行hostname得到的名字

[Reference](http://simplygenius.com/2010/08/jconsole-via-socks-ssh-tunnel.html)