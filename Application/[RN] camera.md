# React Native Expo Camera 사용.
***
## 기본 카메라 설정
`화이트밸런스`, `줌`, 

## VSCO 와 같이 필터 적용하기
페이스북 Jin Ho So님, RECG 앱?
- 구성은 Web-gl과 pixi.js 이용
- 사용 방법: hhtp://github.com/expo/expo-pixi
- [RN으로 인스타 필터 및 편집 유튭](https://youtu.be/AMAJLgafs6U)
- gl-react-expo
- ./gl-filter 사용
## 무음 문제
-  ios has the prop captureAudio as false as default. If you want to capture audio, pass true
read the doc https://github.com/react-native-community/react-native-camera/blob/master/docs/RNCamera.md
- Not on iOS, this is enforced by the operating system. I saw some notes on turning off the shutter sound for Android somewhere. Apparently it's law in Japan that phone cameras must make a sound so that people can't surreptitiously take photos.


### References
- How to mute video capture start/stop sound on Android? #959
https://github.com/react-native-community/react-native-camera/issues/959
- https://
github.com/react-native-community/react-native-camera/issues/1281