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
- ios, android 각각 placement ID 생성 된다.

## 테스트 기기 등록
```js
import * as FacebookAds from 'expo-ads-facebook';

FacebookAds.AdSettings.addTestDevice(FacebookAds.AdSettings.currentDeviceHash);
```

## 광고에 사용할 컴포넌트 선언

**광고를 감싸는 컴포넌트**  
```js
import {
    View,
    StyleSheet,
    Text,
    Dimensions,
    Image,
    TouchableOpacity,
    Platform,
} from 'react-native';
import React, { Component } from 'react';
import * as FacebookAds from 'expo-ads-facebook';]

// 페이스북 광고를 위한 테스트 기기 등록
FacebookAds.AdSettings.addTestDevice(FacebookAds.AdSettings.currentDeviceHash);
const placementId= Platform.OS=='ios'? 'ios 플레이스먼트 아이디':'android 플레이스먼트 아이디'
const numberOfAdsToRequest = 10
const adsManager = new FacebookAds.NativeAdsManager(placementId, numberOfAdsToRequest);


export default class AdContainer extends Component {
    render() {

        return (
            <View
                style={styles.item}
            >
                <AdContent adsManager={adsManager}/>
            </View>
        );
    }
}
```  
  
**광고 컴포넌트**  
```js
import {
    View,
    StyleSheet,
    Text,
    Dimensions,
    Image,
    TouchableOpacity,
    Platform,
} from 'react-native';
import React, { Component } from 'react';
import * as FacebookAds from 'expo-ads-facebook';

const { height, width } = Dimensions.get("window")

class AdContent extends React.Component {
    render() {
        console.log('this.props.nativeAd:',this.props.nativeAd)

      return (
          <Text style={{color:'black'}}>{this.props.nativeAd.advertiserName}</Text>
      );
    }
  }
  
  export default FacebookAds.withNativeAd(AdContent);
```
  
  
**this.props.nativeAd**
```json
this.props.nativeAd: Object {
  "adTranslation": "광고",
  "advertiserName": "Facebook Advertiser",
  "bodyText": "Your ad integration works. Woohoo!",
  "callToActionText": "Install Now",
  "headline": "An ad for Facebook",
  "linkDescription": "Audience Network now supports rewarded video ad format as well. Deliver an immersive in-app ad experience providing users with an incentive in exchange for a completed video view within an interstitial experience.",
  "promotedTranslation": "홍보됨",
  "socialContext": "Available on the App Store",
  "sponsoredTranslation": "Sponsored",
  "target": 889,
}
```