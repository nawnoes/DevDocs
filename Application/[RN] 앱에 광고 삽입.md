# React Native 앱에 광고 삽입.
앱을 통해 수익을 내기 위해서는 리액트 네이티브에서 지원하는 쉬운 방법으로는 광고를 통한 수익과 인앱결제를 통한 수익이 있다. 이 중 facebook ads를 사용한 광고를 붙이도록 한다.

## 광고 종류
크게 Facebook과 Google 2가지로 나뉜다 공식 문서에서는 `Admob` 부분이 Google Ads, `FacebookAds` 부분이 Facebook Ads이다. 이때 앱 내의 이질감 없는 광고를 제공하기 위해 `FacebookAds`의 Native Ads를 사용

## 설치
```
expo install expo-ads-facebook
```

## Placement ID 생성
- Facebook 개발자 사이트에 들어가서 로그인
- 내 앱 행목에서 제품 추가
- Audience Network 등록
- 수익 관리자에서 페이스북 비즈니스 계정 