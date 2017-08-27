React-Native学习指南
https://github.com/reactnativecn/react-native-guide/blob/master/README.md
React Native 研究与实践
https://github.com/crazycodeboy/RNStudyNotes

打包
1.(in project directory) mkdir android/app/src/main/assets
2.react-native bundle --platform android --dev false --entry-file index.android.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res
3.react-native run-android
