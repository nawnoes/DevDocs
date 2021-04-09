# Deview2020 루다 발표 자료 정리
> Deview 2020 이루다 육아일기 발표를 정리한 내용하고자 합니다. 아래의 내용은 https://bit.ly/3mu8YWe 을 정리하며 작성했습니다. 

## 1. 오픈도메인 챗봇
챗봇의 경우 `목적지향형챗봇(Goal-orientedchatbot)` 과 `오픈도메인챗봇(Open-domainchatbot)`으로 나눌 수 있습니다.
- `목적지향형챗봇(Goal-orientedchatbot)`: 특정 주제나 목적에 맞춰 개발 된 챗봇을 말합니다. 예약이나 날씨, 조회 등 편의 성을 기반으로한 챗봇을 말합니다.
- `오픈도메인챗봇(Open-domainchatbot)`: 자유로운 주제에 대해 친구처럼 답할 수 있는 챗봇을 말합니다. 

### 오픈 도메인 챗봇 개발이 어려운이유
#### ① One-to-Many 문제, 하나의 문맥에서 다수의 정답과 다수의 오답이 존재
사람들이 친구들과 대화할때 하나의 문맥에서 여러가지의 선택지에 따른 답변이 있는것을 알수 있습니다. 예를들어 `오늘 뭐할까?` 라는 질문에 대해 운동, 영화, 데이트, 술 등 다양한 주제가 가능하듯 Machine Learning 관점에서 훈련이 어려운 점이 있습니다 
#### ② 대화 데이터 부족 문제
대부분의 언어데이터는 문어체로 구성되어 있어 구어체로 된 대화에는 적합하지 않습니다. 그리고 대화의 특수성 등을 사람들의 실질적인 데이터 셋을 대량으로 구하는데 어려움이 있습니다. 

> 스캐터랩스의 경우 100억건의 한국어 카카오톡 메세지와 10억 일본어 라인 메세지를 학습 데이터로 사용하였다고 합니다. 

## 2. 루다 알파
### 목표
루다는 많은 사람들과 많은대화를 나누는 오픈도메인 챗봇을 개발하는것을 목표로 XiaoIce를 바탕으로 개발을 진행하였습니다.

### XiaoIce
마이크로소프트가 만든 소셜 챗봇으로 웨이보 팔로워 510만명인 중국, 일본, 인도네시아등에 서 활발하게 서비스 되는 오픈도메인 챗봇입니다. 이루다 알파의 프레임워크는 XiaoIce 프레임워크를 기반으로 만들어졌다고 합니다. 

![](https://images.velog.io/images/nawnoes/post/325d3862-427b-4ceb-9bce-c23fb38a6c15/image.png)
>http://aidev.co.kr/chatbot/10003 참고

#### XiaoIce 구조
XiaoIce는 아래와 같이 많은 구성 요소들로 구성되어 있습니다. 
![](https://images.velog.io/images/nawnoes/post/c5eafc56-ec86-48de-bda1-c1319bc758d3/image.png)

### 알파 프레임워크
루다의 알파프레임워크는 아래와 같이 구성되어 있다고 합니다. 
- 보라색 부분은 사용자의 말을 이해하는 `NLU` 
- 하얀 부분은 답변 및 답변 후보 생성을 위한 `Retrieval`
- 노란 부분은 후보 답변 중 최종 답변 결정을 위한 `Ranker`
![](https://images.velog.io/images/nawnoes/post/b6e06b32-23c2-43af-b58e-f43a9476b89d/image.png)
#### NLU
대화를 이해하는 부분으로 DialogBERT, Emotion, Dialogue Act, Engage Mode, Topic들로 구성되어 있습니다. 
#### Retrieval 
1차로 응답하기 위한 후보를 가져오는 부분입니다. 
- ① 세션과 답변으로 구성된 `Session DB`를 통해 현재 대화와 유사한 세션들로 응답 후보로 선정합니다.
- ② 주제어를 포함한 문장형태로 구성된 `Content DB`를 통해 현재 대화의 주제ㅓ를 포함한 응답을 후보로 선정합니다. 
#### Ranker
응답 후보 중 가장 적합한 대답을 선정하는 부분입니다. Response Selection([Poly-Encoder](https://roomylee.github.io/poly-encoder/)), Discourse Matching, 기타 Feature들로 구성되어 적절한 대답을 선정하는 부분입니다. `Poly-Encoder`의 경우

##### Poly-encoder

응답을 선택하는 부분에서 루다에서 사용한 방법입니다. [Poly-Encoder 정리 블로그](https://roomylee.github.io/poly-encoder/)에 잘 정리 되어 있어, 참고하면 좋을것 같습니다. Poly-Encoders는 답변 문장을 선택하기 위해 문장을 비교하는 방식입니다. 

![](https://images.velog.io/images/nawnoes/post/44e17fc2-917a-4165-b016-78fc44cb212f/image.png)

기존에 문장을 비교하는 태스크에서 문장 쌍을 한번에 인코딩하는 `Cross-encoder` 방식과 각각 인코딩하는 `Bi-encoding` 방식이 있습니다. `Cross-encoder`의 경우 두 문장의 쌍을 한번에 인코딩하기 때문에 성능은 좋지만 속도가 느린 단점이 있습니다. `Bi-encoding`의 경우 각문장에 대해서 인코딩해 속도가 빠르지만 성능은 안좋은 단점이 있습니다. 

위와 같은 `Bi-encoding`과 `Cross-encoder`을 보완하기 위해 Poly-encoder을 사용하였고, Poly-encoder는 4개 태스크에 대해 SOTA를 달성했다고 합니다. 따로 좀더 찾아보아도 좋을것 같습니다. 

### 성능평가, SSA
#### 작성중..🏃‍♂️
## 3. 루다 베타
## 4. 

# References
- https://roomylee.github.io/poly-encoder/
- https://bit.ly/3mu8YWe