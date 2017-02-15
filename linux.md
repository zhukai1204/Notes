全局替换 %s/xxx/xxx/g

遍历目录并并执行相应操作 find . -name "*.c" -exec ls {} \;

统计当前文件夹下文件的个数，包括子文件夹里的 
ls -lR|grep "^-"|wc -l
