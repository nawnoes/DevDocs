## 멀티 태스크 & 메타러닝 기초
### 다루는 주제
#### 멀티 태스크 러닝
- 멀티태스크 러닝에서 다루는 모델과 아키텍처
- 학습 알고리즘들과 실제 어떻게 학습하는 지
- 그 과정에서 발생하는 문제
- 실제 사례 연구
#### 메타 러닝
- 문제 공식화: 첫 강의에서는 대략적으로(informal) 메타러닝 태스크에 대해 설명하였고, 그 부분을 공식화 한다. 
- 일반적으로 메타러닝을 다루는 방법
- `Black Box Adaptation`이라는 메타러닝 알고리즘에 대해 배움.

### 1. Multi-Task Learning
#### 1.1 Notation
![](https://images.velog.io/images/nawnoes/post/a0d24e98-d980-46a5-8f16-52b95c22bd91/image.png)
- 신경망은 입력 x 를 받아 y를 출력
- 입력이 주어지면 출력 y에 대한 분포가 생성된다.
- 입력에 따라 y가 항상 분포(distribution)이 되는게 아닌 결정론적(deterministic)이 될 수도 있다. 
##### Single-task Learning에서의 예
- 어떠한 데이터 $\mathcal{D} =\{{(x,y)_k}\}$가 주어져 있고.
- 손실함수(Loss Function) $\mathcal{L}(\theta,\mathcal{D})$
- 신경망의 웨이트 $\theta$

위와 같을 때,손실함수 $\mathcal{L}(\theta,\mathcal{D})$를 최소화 하는 웨이트 $\theta$를 찾는 것. 
- 일반적으로 손실함수는 negative log likelihood를 사용하며, 역전파을 이용해서 학습한다.    
 $\mathcal{L}(\theta,\mathcal{D}) = E_{(x,y)\sim\mathcal{D}}[logf_{\theta}(y|x)]$
 
##### Multi-task learning에서의 Task란?
$\mathcal{T}_i \triangleq \{p_i(x), p_i(y|x), \mathcal{L}_i\}$ 과 같이 Task 를 정의 한다.
- 입력 x 에 대한 분포
- 입력값과 손실 함수가 distributions으로 나타나며
- 데이터는 distribution들을 생성한다.

Dataset은 $\mathcal{D}_i^{tr}$, $\mathcal{D}_i^{test}$으로 구성되며, 일반적으로 강의에서 $\mathcal{D}_i$는 $\mathcal{D}_i^{tr}$을 의미한다. 

#### 1.2 Multi-task Learning에서 Task의 예
위와 같이 정의한 Task에 대해서 아래의 예를 통해 설명하고자 한다. 
  
**Task**
$\mathcal{T}_i \triangleq \{p_i(x), p_i(y|x), \mathcal{L}_i\}$ 과 같이 Task 를 정의 한다.
- 입력 x 에 대한 분포
- 입력값과 손실 함수가 distributions으로 나타나며
- 데이터는 distribution들을 생성한다.

Dataset은 $\mathcal{D}_i^{tr}$, $\mathcal{D}_i^{test}$으로 구성되며, 일반적으로 강의에서 $\mathcal{D}_i$는 $\mathcal{D}_i^{tr}$을 의미한다. 

##### 1) Multi-task Classification
다중 분류 작업의 경우 모든 태스크들에 대해서 손실함수 $\mathcal{L}_i$는 동일하며, 손실함수의 경우 크로스엔트로피를 사용한다.
  
사용예로는
- 언어별, 손글씨 인식
- 개인화된 스팸필터: 사람마다 스팸의 기준이 다르므로 스팸의 유형이 달라지게 된다. 그래서 사람 간 스팸 분류는 다르게 될 수 있가. 이때 $p_i(x)$는 이메일의 타입이 다르기 때문에 서로다른 $p_i(x)$를 갖게 되고, 그에 따라 분류가 달라지게 된다. 
##### 2) Multi-label learning
$\mathcal{L}_i$와 $p_i(x)$는 모든 태스크들에 대해서 동일하다. 다른점은 라벨에 대해 예측을 하길 원하는 것으로 예로는 아래와 같은 것들이 있다. 
- 속성인식: 사람이 모자를 쓰고 있는지, 머리색 깔이 다른지
- Scene Undeerstanding: 카메라가 보는 장면의 깊이나 

이러한 설정은 손실함수는 같으며, 데이터의 distribution만 달랐다. 
## References
- [CS330 lecture2](https://www.youtube.com/watch?v=6stKGH6zI8g&list=PLoROMvodv4rMC6zfYmnD7UG3LVvwaITY5&index=2)
- [CS330 2019](http://cs330.stanford.edu/fall2019/index.html)