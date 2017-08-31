<pre>
  function fetchPost(url ,data) {    
      let host = DIX.HOST + url;    
      let token = UTIL.getToken();    
      let dataUrl = '';    
      if (data)  {        
          for (let item in data)  {            
            if (data.hasOwnProperty(item))  {                
                dataUrl += ('&' + item + '=' + data[item]); 
            }        
          }    
      }    
      let body = 'client=1&version=3&token=' + token + dataUrl;    

      return fetch (host, { 
          method: 'POST',        
          headers: {            
              "Content-Type": "application/x-www-form-urlencoded" 
          },        
          body: body    
      }).then(function(res) {        
          if (res.status !== 200) {            
              console.log('Looks like there was a problem. Status Code: ' + res.status);           
              return;       
           }        
          // 处理响应中的文本信息        
          return res.json();    
      }).catch(function(err) {      
          console.log('Fetch Error : %S', err);   
       })
  }
</pre>

React-Native学习指南</br>
https://github.com/reactnativecn/react-native-guide/blob/master/README.md</br>
React Native 研究与实践</br>
https://github.com/crazycodeboy/RNStudyNotes</br>

打包</br>
1.(in project directory) mkdir android/app/src/main/assets</br>
2.react-native bundle --platform android --dev false --entry-file index.android.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res</br>
3.react-native run-android</br>
