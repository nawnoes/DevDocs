# Expo, React-Native App 배포

## 1. Expo 
expo란 react-native 초심자를 위해 빠르게 프로젝트를 시작할 수 있게 하는 도구. 기존에 react-native-create-app에서 변경

## 2. Expo 배포 과정

1. 완성된 프로젝트 빌드 후 standalone softwaree파일 생성
    > andoid는 **apk**파일, ios는 **ipa**파일
2. 생성된 apk와 ipa 파일을 **실제 기기**, **에뮬레이터**에서 테스트
3. **google play store**와 **Apple app store**에 등록 및 배포
4. 지속 업데이트
  
## 3. 세부 배포 과정
[공식문서](https://docs.expo.io/versions/latest/distribution/building-standalone-apps/?redirected) 참조

### Expo CLI 설치
expo build에 필요한 명령어를 위해 설치
```
npm install -g expo-cli
```

### app.json 설정
배포에 대한 환경 설정을 위해 expo init [프로젝트 이름]으로 생성한 프로젝트 내, app.json을 수정

> 옵션에 대한 링크는 [Configuration app.json](https://docs.expo.io/versions/latest/workflow/configuration/) 확인

```
{
   "expo": {
    "name": "Your App Name",
    "icon": "./path/to/your/app-icon.png",
    "version": "1.0.0",
    "slug": "your-app-slug",
    "sdkVersion": "XX.0.0",
    "ios": {
      "bundleIdentifier": "com.yourcompany.yourappname"
    },
    "android": {
      "package": "com.yourcompany.yourappname"
    }
   }
 }
```

### 앱빌드
build를 통해 stanalone 파일(apk, ipa)을 생성
> **-c**옵션을 통해 캐시를 삭제하므로, 기존의 인증서 정보를 삭제할 수 있다.

**iOS**
```
expo build:ios
```
**android**
```
expo build:android
```
두 경우 모두 최초 프로젝트 빌드시, **인증서** 부분에 대한 메세지가 나온다.  
   - 1번은 배포에 관한 인증서 파일들을 expo에서 새로 만들어서 등록 및 관리 
   - 2번은 기존에 배포된 프로젝트나 인증서를 새로 생성할 수 없는 경우 사용
**ios**
    apple store ID, Password, ios배포인증서 .p12 파일, 푸시 알람 인증서 .p12파일, 프로비저닝 .mobileprovision파일이 순서대로 필요.
**android**
    play store ID, password, .jks 인증서 파일
  

위 내용 중 유효하지 않는 내용이 있다면 build 실패

# Reference
https://medium.com/encored-technologies-engineering-data-science/expo-react-native-create-app-%EC%9C%BC%EB%A1%9C-%EC%95%B1%EC%8A%A4%ED%86%A0%EC%96%B4%EC%97%90-%EB%B0%B0%ED%8F%AC%ED%95%98%EA%B8%B0-d1c9af5c8802