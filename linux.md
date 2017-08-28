<pre>
查看端口占用情况
直接使用 netstat   -anp   |   grep  portno
即：netstat –apn | grep 8080

全局替换 %s/xxx/xxx/g

遍历目录并并执行相应操作 find . -name "*.c" -exec ls {} \;

统计当前文件夹下文件的个数，包括子文件夹里的 
ls -lR|grep "^-"|wc -l

当前目录下查找字符
grep -rn 'name' ./
</pre>
