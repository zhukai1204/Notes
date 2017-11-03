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
    <a href="https://www.mongodb.com/download-center#community"  target="_blank">查看最新版</a>
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
    
    centos nvm 安装
    wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.30.1/install.sh | bash
    source ~/.bash_profile
    通过nvm安装管理nodejs
    1、列出所有可安装的版本nvm list-remote；
    2、安装相应的版本使用nvm install v0.12.4；还可以直接安装 iojs 各个版本；
    3、查看一下你当前已经安装的版本:nvm ls；
    4、切换版本；nvm use v0.12.4；
    5、设置默认版本 nvm alias default v0.12.4
    注意：具体操作很简单，使用帮助通过nvm help；
    
    
    #安装gcc
    yum -y install gcc
    #下载redis
    curl -O  http://download.redis.io/releases/redis-3.2.8.tar.gz
    #解压
    tar -zxvf redis-3.2.8.tar.gz
    #转换目录
    cd redis-3.2.8/deps/
    #编译依赖
    make geohash-int hiredis jemalloc linenoise lua
    #转换目录
    cd ..
    #编译Redis
    make && make install
    #转换目录
    cd utils/
    #使用脚本安装服务
    ./install_server.sh
    #启动服务
    systemctl start redis_6379
    systemctl status redis_6379
    
    Please select the redis port for this instance: [6379] yes
    Selecting default: 6379
    Please select the redis config file name [/etc/redis/6379.conf] y
    Please select the redis log file name [/var/log/redis_6379.log] y
    Please select the data directory for this instance [/var/lib/redis/6379] y
    Please select the redis executable path [/usr/local/bin/redis-server] y
    Selected config:
    Port           : 6379
    Config file    : y
    Log file       : y
    Data dir       : y
    Executable     : /usr/local/bin/redis-server
    Cli Executable : /usr/local/bin/redis-cli
    Is this ok? Then press ENTER to go on or Ctrl-C to abort.
    Copied /tmp/6379.conf => /etc/init.d/redis_6379
    Installing service...
    Successfully added to chkconfig!
    
    启动服务
    Redis-server redis.conf
    关闭服务
    redis-cli shutdown

    客户端启动
    redis-cli
    
    #安装git
    1.安装编译git时需要的包
    # yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
    # yum install  gcc perl-ExtUtils-MakeMaker
    2.删除已有的git
    # yum remove git
    3.下载git源码，我自己下载的是2.0.0版本的下载地址：http://pan.baidu.com/s/1qXFnOxI
    # cd /usr/src
    <a href="https://git-scm.com/" target="_blank">查看最新版本</a>
    # wget https://www.kernel.org/pub/software/scm/git/git-2.0.5.tar.gz
    # tar xzf git-2.0.5.tar.gz
    4.编译安装
    # cd git-2.0.5
    # make prefix=/usr/local/git all
    # make prefix=/usr/local/git install
    # echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/bashrc
    # source /etc/bashrc
    5.检查一下版本号
    # git --version
    
    Phantomjs 安装
    <a href="http://phantomjs.org/download.html">Phantomjs最新版</a>
    #wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2

    #tar -xjvf phantomjs-1.9.7-linux-x86_64.tar.bz2

    将可执行文件放入系统路径：　

     #sudo ln -s ~/bin/phantomjs-1.9.7-linux-x86_64/bin/phantomjs /usr/local/bin/phantomjs

    安装依赖——fontconfig和freetype：　

     #yum install fontconfig freetype2

    CentOS - 执行phantomjs报错
    报错信息：phantomjs: error while loading shared libraries: libfreetype.so.6: cannot open shared object file: No such file     or directory
    解决方法：
    执行
    # sudo yum install freetype
    如果还报错
    执行
    # sudo yum install fontconfig freetype libfreetype.so.6 
    如果使用 ubuntu  或者 debian
    use apt-get install to install this package

</pre>
