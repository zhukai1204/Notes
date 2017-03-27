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
</pre>
