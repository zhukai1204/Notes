React-Native学习指南</br>
https://github.com/reactnativecn/react-native-guide/blob/master/README.md</br>
React Native 研究与实践</br>
https://github.com/crazycodeboy/RNStudyNotes</br>

打包</br>
1.(in project directory) mkdir android/app/src/main/assets</br>
2.react-native bundle --platform android --dev false --entry-file index.android.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res</br>
3.react-native run-android</br>
