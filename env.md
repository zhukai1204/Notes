<pre>
一.centos下面安装node
  1.安装编译需用的工具
    yum -y install gcc gcc-c++ kernel-devel
  2.获取nodejs并解压
    wget https://nodejs.org/dist/v4.5.0/node-v4.5.0.tar.gz
    tar -xf node-v4.5.0.tar.gz
  3.编译和安装
    cd node-v4.5.0
    ./configure
    make
    sudo make install
  4.需要更新可以更新到最新版
    npm install -g n
    n stable
 二.centos安装mongodb
  1.获取mongodb
    wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.2.6.tgz
  2.解压安装
    tar zxvf mongodb-linux-x86_64-3.2.6.tgz
    mv mongodb-linux-x86_64-3.2.6.tgz mongodb
    cd mongodb
    mkdir db
    mkdir logs
    cd bin
    vi mongodb.conf
    复制代码
    dbpath=/usr/local/mongodb/db
    logpath=/usr/local/mongodb/logs/mongodb.log
    port=27017
    fork=true
    nohttpinterface=true
    重新绑定mongodb的配置文件地址和访问IP

    /usr/local/mongodb/bin/mongod --bind_ip localhost -f /usr/local/mongodb/bin/mongodb.conf


    复制代码
    开机自动启动mongodb

    vi /etc/rc.d/rc.local
    /usr/local/mongodb/bin/mongod --config /usr/local/mongodb/bin/mongodb.conf
    重启一下系统测试下能不能自启

    #进入mongodb的shell模式 
    /usr/local/mongodb/bin/mongo
    #查看数据库列表 
    show dbs
    #当前db版本 
    db.version();
    
    
    pm2启动sails
    pm2 start app.js -x -- --prod
    <a href="http://sailsjs.com/documentation/concepts/deployment">deployment</a>
</pre>
