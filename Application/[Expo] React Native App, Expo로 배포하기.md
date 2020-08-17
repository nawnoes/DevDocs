# react native expo로 앱 배포하기

## 기본 앱 배포 과정
1. 완성된 앱을 빌드하여, standalone 파일로 변환
    - android는 `apk`
    - ios는 `ipa`
    > standalone 파일은 expo의 서버 연결 없이, 설치 파일로써 기기에서 동작하는 파일을 말한다
    > 앱 빌드를 위해서는 인증서를 발급 받아야 한다.

## 1. IOS
### 1.1. 인증서 사전 지식
- Certificates: 누가 앱을 개발하거나 배포할것인지 나타내는 인증서
    + All
    + Pending
    + Development: 앱을 만들고 테스트할 사람이 누구인지 밝히는 인증서
    + Production: 앱스토어에 실제로 배포할 사람이 누구인지를 밝혀주는 인증서

- Key: 인증서와 연계되는 Key로 배포에서 크게 살펴볼일이 없었다.
- Identifiers: 무엇을 개발할지를 나타내는 식별자 
    + AppIDs: 개발한 expo 앱을 등록하고, `고유의 ID` 값을 받는다. `.ipa`파일을 만들기 전에 expo의 app.json 파일에 bundleIdentifier 속성을 직접 기재하는데, 이때 AppID 메뉴에서 이 값을 사용하게 된다. 
    + PassTypeIDs
    + WebsitePushIDs
    + iCloud Containers
    + App Groups
    + Merchant IDs
    + Music IDs
    + Maps IDs
- Devices: 어디서 앱을 실행할지 나타내는 장치 목록
    + All
    + AppleTV
    + Apple Watch
    + iPad
    + iPhonee
    + iPod Touch
- Provisionining Profiles: `누가`, `무엇`을, `어디서`할 지에 대한 모든 정보를 갖고 있는 정보.
    + All
    + Development: 실제 모바일 폰에서 만들어진 앱을 테스팅 할 때, 필요한 정보
        * 이 정보는 Certificates의 development cerificates/ Identifiers의 App ID/ Devices의 총 3가지 정보가 기입해야 생성할 수 있다.
    + Distribution: 실제 앱스토어에 배포 후 사용자들에게 분배할 때 필요한 정보.
        * Certificates의 distribution certificates/ Identifiers의 App ID 두가지 정보만을 필요로 한다. 

### 1.2. Expo에서 .ipa 파일을 만들기 위해 필요한 인증 파일들
앱을 배포하기 위해서는 3가지 파일이 필요하다.
1. distribution certificate와 개인키로 만들어진 `.p12`파일
2. push notification certificate와 개인키로 만들어진 `.p12`파일
3. distribution provisioning profile을 나타내는 `.mobileprovision`파일
    > `.p12`는 애플에서 발급한 인증서와 인증서에 접근할수 있는 인증서와 인증서에 접근할 수 있는 권한을 갖고 있는사람인지 증명하는 개인키가 한쌍이 되어 만들어진 하나의 파일 
    > 현대의 디지털 인증은 X.509 표준을 따르며, 애플의 signing이나 웹의 인증 모두 그 표준 위에 세워진 PKI
### 1.3. 필요한 파일들 생성하기
1. 애플 아이디 생성
2. 애플 아이디로 애플 개발자 프로그램에 등록
    : 위 3 파일들을 만들기 위해서는 애플 개발자 프로그램에 등록이 필요하다.
**구매**  
![](https://images.velog.io/images/nawnoes/post/2a78a88b-171c-45c2-a829-8f4764ba1fa1/image.png)
> 가격이 ㄷㄷㄷ

**구매완료**  
크롬으로 결제하는 경우 오류가 발생하여, 개발자 지원 센터의 도움으로`사파리` 최신버전에서 재 진행. 사파리에서 진행 후 결제 완료.
![](https://images.velog.io/images/nawnoes/post/c9e0d6f2-3ac6-4920-8a86-27bf0c0135cf/image.png)

**대기**  
가이드 대로 최대 48까지 기다려야 하나보다..
![](https://images.velog.io/images/nawnoes/post/9f7e7187-e357-4e4e-bf75-a6c9c33cc1b8/image.png)

### ... 인증이 될때까지 기다려보자
### (작성중)
## 2. Android


# References
- [[EXPO(react-native-create-app) 프로젝트 배포] 2. ios, android 별로 필요한 인증 파일 생성하기](https://medium.com/duckuism/expo-react-native-create-app-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%B0%B0%ED%8F%AC-2-ios-android-%EB%B3%84%EB%A1%9C-%ED%95%84%EC%9A%94%ED%95%9C-%EC%9D%B8%EC%A6%9D-%ED%8C%8C%EC%9D%BC-%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0-d917f31d8d9f)
- [ios-앱-배포-과정-1](https://velog.io/@yejinh/ios-%EC%95%B1-%EB%B0%B0%ED%8F%AC-%EA%B3%BC%EC%A0%95-1)