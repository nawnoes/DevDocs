# React-Native Push 
![](https://images.velog.io/post-images/max9106/14a21050-e38d-11e9-918b-73ab88e7b3a8/-2019-09-30-11.17.39.png)

- 로컬 서버를 인터넷에 노출시키는 역할인 ngrok를 설치
- es6 문법을 서버에서 사용하기 위해 esm push 알람을 진행하기 위한 expo-server-sdk를 설치
- permission을 위한 expo install expo-permissions를 설치

# 1. Expo Push Notification
Expo Push Notification을 사용해서 ios와 android로 보낼 푸시 메세지를 구현. expo에서 제공는 push sdk(node js)를 이용해 푸시 시스템 생성.

## 1.1 Push Notification Sequence Diagram
Push 시스템의 과정
App     Server     Admin     Push Server
 |        |          |            |
 |        |          |            |
 |        |          |            |

    1) 앱실행
    2) 클라이언트에서 서버로 푸시 토큰 및 앱 정보 저장 API 호출
    3) 서버는 푸시 토큰 및 앱 정보를 저장
    4) 서버에서 클라이언트로 푸쉬 토큰 및 앱 정보 결과를 반환
    5) Admin에서 푸쉬 발송 옵션 및 대상 설정
    6) Admin에서 Server로 푸쉬 발송 API 전달
    7) 서버에서 푸쉬 발송 대상자 목록화 
    8) Server에서 Push Server에 푸쉬 요청 API 호출
    9) Push Server에서 APNS, FCM에 전달
    10) Push Server에서 Server에 푸시 결과 저장 API 호출
    11) Server에서 푸쉬 결과 DB 저장
    12) Admin에서 푸쉬 결과 확인 및 '재'발송

## 1.2 Push Token 생성
> 푸시토큰은 Application 단위로 생성
> Application을 삭제 후 재설치하게 되면 푸시토큰이 변경
> Expo 푸쉬는 디바이스에서만 수신
   



# Ref
- [Expo 공식 홈페이지](https://docs.expo.io/versions/latest/guides/push-notifications/)
- https://velog.io/@max9106/React-Native-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8Creact-native-%ED%91%B8%EC%8B%9C%EC%95%8C%EB%9E%8C-expo-jkk16hzg5d