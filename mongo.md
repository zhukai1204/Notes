<pre>
1.下载安装包
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel62-3.2.9.tgz
下载完成后解压缩压缩包
tar zxf mongodb-linux-x86_64-rhel62-3.2.9.tgz
 
2. 安装准备
将MongoDB文件夹命名为mongdb文件夹
mv mongodb-linux-x86_64-rhel62-3.2.9 mongodb
 
创建数据库文件夹与日志文件
mkdir /home/mongodb/data
mkdir /home/mongodb/logs
touch(创建文件)
3. 启动mongodb
cd到mongodb目录下的bin文件夹启动mongodb
//下面这个是需要权限的登录方式, 用户连接需要用户名和密码
./mongod --dbpath=/home/mongodb/data --logpath=/home/mongodb/logs --logappend  --auth  --port=27017 --fork
//这个是不需要密码的
./mongod --dbpath=/home/mongodb/data --logpath=/home/mongodb/logs --logappend  --port=27017 --fork
或者
在mongodb下面创建文件 my.cnf
touch my.cnf
里面内容为:
.
port=27017
dbpath=/home/mongodb/data
logpath=/home/mongodb/logs/mongodb.log
pidfilepath=/home/mongodb/mongo.pid
fork=true
logappend=true
#auth=true
保存完后，回到bin目录下，输入
 ./mongod --config /home/mongodb/my.cnf
。
5，查看进程。
netstat -lanp |grep 27017
6，创建用户
进入bin目录下，  输入./mongo 127.0.0.1:27017 连接到mongodb中，
输入use test （MongoDB use DATABASE_NAME 用于创建数据库。该命令将创建一个新的数据库，如果它不存在，否则将返回现有的数据库。）
创建用户名，密码和角色。
 db.createUser({user:"testuse",pwd:"1qaz@wsx",roles:[{role:"readWrite",db:"picadb"}]})
至此，用户和密码已创建完毕。
7，重新启动mongodb。查看mongodb。
修改刚才的my.cnf文件，在内容中添加 auth=true。 保存。
重启mongodb，再登录到mongodb中，
[root@iZ253cglmsxZ bin]# ./mongo 127.0.0.1:27017
MongoDB shell version: 3.2.9
connecting to: 127.0.0.1:27017/test
> use test
switched to db test
> show collections
2016-09-05T16:46:13.013+0800 E QUERY    [thread1] Error: listCollections failed: {
"ok" : 0,
"errmsg" : "not authorized on picadb to execute command { listCollections: 1.0, filter: {} }",
"code" : 13
} :
_getErrorWithCode@src/mongo/shell/utils.js:25:13
DB.prototype._getCollectionInfosCommand@src/mongo/shell/db.js:773:1
DB.prototype.getCollectionInfos@src/mongo/shell/db.js:785:19
DB.prototype.getCollectionNames@src/mongo/shell/db.js:796:16
shellHelper.show@src/mongo/shell/utils.js:754:9
shellHelper@src/mongo/shell/utils.js:651:15
@(shellhelp2):1:1

> db.auth("testuser","1qaz@wsx")
1
> show collections
movie
查看成功表明 mongodb用户名和密码创建成功。



本文我们介绍MongoDB权限管理，主要介绍的是如何设置用户名和密码。接下来我们就一一介绍。  
  
添加用户的时候必须满足以下两个条件：  
  
1.有相关权限的情况下（后面会说）。  
  
2.mongod没有加--auth的情况下（如果加了,你添加权限的话 会出现下面的情况）。  
  
  
> use admin      
   
switched to db admin      
   
> db.addUser('sa','sa')      
   
Fri Jul 22 14:31:13 uncaught exception: error {      
   
"$err" : "unauthorized db:admin lock type:-1 client:127.0.0.1",      
   
"code" : 10057      
   
}      
   
>      
所以我们添加用户时必须先在没有加--auth的时候添加个super  admin。  
  
服务起来后，进入./mongo。  
  
  
[root@:/usr/local/mongodb/bin]#./mongo      
   
MongoDB shell version: 1.8.2      
   
connecting to: test      
   
> use admin      
   
switched to db admin      
   
> db.adduser('sa','sa')      
   
Fri Jul 22 14:34:24 TypeError: db.adduser is not a function (shell):1      
   
> db.addUser('sa','sa')      
   
{      
   
"_id" : ObjectId("4e2914a585178da4e03a16c3"),      
   
"user" : "sa",      
   
"readOnly" : false,      
   
"pwd" : "75692b1d11c072c6c79332e248c4f699"      
   
}      
   
>      
这样就说明 已经成功建立了，然后我们试一下权限。  
  
  
> show collections      
   
system.indexes      
   
system.users     
在没有加--auth的情况下 可以正常访问admin喜爱默认的两个表。  
  
  
> db.system.users.find()      
   
{ "_id" : ObjectId("4e2914a585178da4e03a16c3"), "user" : "sa", "readOnly" : false, "pwd" : "75692b1d11c072c6c79332e248c4f699" }>      
已经成功建立。  
  
下面把服务加上--auth的选项，再进入./mongo。  
  
  
MongoDB shell version: 1.8.2      
   
connecting to: test      
   
> use admin      
   
switched to db admin      
   
> show collections      
   
Fri Jul 22 14:38:49 uncaught exception: error: {      
   
"$err" : "unauthorized db:admin lock type:-1 client:127.0.0.1",      
   
"code" : 10057      
   
}      
   
>      
可以看出已经没有访问权限了。  
  
我们就用自己的密钥登录下：  
  
  
> db.auth('sa','sa')      
   
1     
返回1说明验证成功！  
  
再show collections下就成功了。  
  
.....  
  
我们登录其它表试试：  
  
  
[root@:/usr/local/mongodb/bin]#./mongo      
   
MongoDB shell version: 1.8.2      
   
connecting to: test      
   
> use test      
   
switched to db test      
   
> show collections      
   
Fri Jul 22 14:40:47 uncaught exception: error: {      
   
"$err" : "unauthorized db:test lock type:-1 client:127.0.0.1",      
   
"code" : 10057      
   
}     
也需要验证，试试super admin登录：  
  
  
[root@:/usr/local/mongodb/bin]#./mongo      
   
MongoDB shell version: 1.8.2      
   
connecting to: test      
   
> use test      
   
switched to db test      
   
> show collections      
   
Fri Jul 22 14:40:47 uncaught exception: error: {      
   
"$err" : "unauthorized db:test lock type:-1 client:127.0.0.1",      
   
"code" : 10057      
   
}      
   
> db.auth('sa','sa')      
   
0     
返回0验证失败。   
  
好吧，不绕圈子，其实super admin必须从admin那么登录 然后 再use其它表才可以。  
  
  
> use admin      
   
> use admin    
   
switched to db admin      
   
> db.auth('sa','sa')      
   
1      
   
> use test      
   
switched to db test      
   
> show collections      
   
>      
如果想单独访问一个表，用独立的用户名，就需要在那个表里面建相应的user。  
  
  
[root@:/usr/local/mongodb/bin]#./mongo      
   
MongoDB shell version: 1.8.2      
   
connecting to: test      
   
> use admin      
   
switched to db admin      
   
> db.auth('sa','sa')      
   
1      
   
> use test      
   
switched to db test      
   
> db.addUser('test','test')      
   
{      
   
"user" : "test",      
   
"readOnly" : false,      
   
"pwd" : "a6de521abefc2fed4f5876855a3484f5"      
   
}      
   
>      
当然必须有相关权限才可以建立。  
  
再登录看看：  
  
  
[root@:/usr/local/mongodb/bin]#./mongo      
   
MongoDB shell version: 1.8.2      
   
connecting to: test      
   
> show collections      
   
Fri Jul 22 14:45:08 uncaught exception: error: {      
   
"$err" : "unauthorized db:test lock type:-1 client:127.0.0.1",      
   
"code" : 10057      
   
}      
   
> db.auth('test','test')      
   
1      
   
> show collections      
   
system.indexes      
   
system.users      
   
>     
mongodb数组操作
http://howsun.blog.sohu.com/305176472.html
https://www.pocketdigi.com/20130526/1084.html
</pre>
