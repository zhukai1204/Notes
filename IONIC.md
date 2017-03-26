<pre>
ionic2安装时遇到There was an error with the spawned command: npminstall  
跳过node_module安装ionic start app --v2 --skip-npm

config.xml
Android平台对应的文件路径为：MyProject/platforms/android/res/xml/config.xml
iOS平台对应的文件路径为：MyProject/platforms/ios/MyProject/config.xml
widget:id填写app所有人的域名，version填写app的版本号

name：app名称，该名称会出现在设备主页上或者应用程序商店的程序清单中

description：app描述，会在app stroe里显示

author：app作者相关信息，会在app stroe里显示

content：指定app开始指向页面,应用的入口文件（可选的，默认为index.html）

access：指定app可进行通信的域名，*为所有

可以设置多个： 
<access origin="http://example.com"/> 
<access origin="http://foobar.example.com"/> 
也可以使用通配符： 
<access origin="http://*.example.com"/> 
默认可以访问任何域： 
<access origin="*"/>
preference：偏好设置，可针对不同平台进行个性化设置。

设置程序是否全屏。全屏时状态栏将不可见，默认为false
<preference name="Fullscreen" value="true" />

横屏竖屏锁定。可选的值有：default，landscape，portrait
如果你想针对不同的平台进行不同的设置，请将此配置节从根目录下的config.xml中移除。
<preferencename="Orientation" value="landscape" />

隐藏滚动条，默认值为false，适用于android、ios：
<preference name="DisallowOverscroll" value="true"/>

背景色设置，适用于android、BlackBerry，可在CSS中设置body的背景色替代该方法且对所有平台都适用：
<preference name="BackgroundColor" value="0xff0000ff"/>

隐藏键盘上的工具栏，适用于iOS、BlackBerry：
<preference name="HideKeyboardFormAccessoryBar" value="true"/>

针对指定平台设定横竖屏，适用于Android、iOS、WP8、Amazon Fire OS、Firefox OS：
<platform name="android">
     <preference name="Orientation" value="sensorLandscape" />
</platform>
在ios平台下，可通过JS控制：
function shouldRotateToOrientation(degrees) {
     return true;
}

针对特定平台设置：
<platform name="android">
      <preference name="Fullscreen" value="true" />
</platform>

android配置：
<preference name="KeepRunning" value="false"/>
<preference name="LoadUrlTimeoutValue" value="10000"/>
<preference name="SplashScreen" value="mySplash"/>
<preference name="SplashScreenDelay" value="10000"/>
<preference name="InAppBrowserStorageEnabled" value="true"/>
<preference name="LoadingDialog" value="My Title,My Message"/>
<preference name="LoadingPageDialog" value="My Title,My Message"/>
<preference name="ErrorUrl" value="myErrorPage.html"/>
<preference name="ShowTitle" value="true"/>
<preference name="LogLevel" value="VERBOSE"/>
<preference name="AndroidLaunchMode" value="singleTop"/>
feature:应用中使用了哪些Native功能，Cordova在运行时会扫描feature属性就知道哪些Plugin是有效的。在执行cordova plugin add的时候会自动添加feature

生命周期函数
----------------------------------------
 ##文件下载##
    $scope.openLinkInBrowser = function (url) {
      // Show the action sheet
      var hideSheet = $ionicActionSheet.show({
        buttons: [
          { text: '<center>保存</center>' }
        ],
        // destructiveText: 'Delete',
        titleText: '<center>保存图片？</center>',
        cancelText: '<center>Cancel</center>',
        cancel: function () {
          // add cancel code..
        },
        buttonClicked: function (index) {
          var filename = url.split("/").pop();
          var targetPath = cordova.file.externalRootDirectory + "DCIM/" + filename;
          $cordovaFileTransfer.download(encodeURI(url), targetPath, {}, true)
            .then(function (result) {
              $ionicPopup.alert({
                title: '<b>图片保存成功</b>',
                subTitle: '<img src="img/hh.png">',
                buttons: [{
                  text: '嗯',
                  type: 'button-positive',
                  onTap: function (e) {

                  }
                }]
              })
            }, function (err) {
              alert(angular.toJson(err));
            }, function (progress) {
              $timeout(function () {
                $scope.downloadProgress = (progress.loaded / progress.total) * 100;
              });
            });
          return true;
        }
      });

    }
##########################################################
ionic2
typescript https://www.gitbook.com/book/zhongsp/typescript-handbook/details
typescript sublime 语法高亮 http://blogs.msdn.com/b/interoperability/archive/2012/10/01/sublime-text-vi-emacs-typescript-enabled.aspx

angular2  https://angular.cn/
</pre>
