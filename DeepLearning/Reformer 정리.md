# Reformer 정리
# 1. Reformer 개요
> [Illustrating the Reformer](https://towardsdatascience.com/illustrating-the-reformer-393575ac6ba0)를 보며 정리.


리포머 모델을 2020년에 발표된 모델로 기존 트랜스포머 구조를 개선한 모델이다. `Local Sensitve Hashing`과 `Reversible residual network`를 이용해 이전 트랜스 포머 보다 더 많은 입력을 사용할 수 있으며, 낮은 메모리 사용량을 가지면서 거의 유사한 성능을 내는 모델이다. 논문의 저자는 **텍스트** 뿐만아니라 **이미지**에도 실험해보았다.

## 트랜스포머 모델 구조의 단점.
트랜스포머 모델이 뛰어난 성능을 가지더라도. 뛰어난 성능을 내는 모델들은 매우 뛰어난 컴퓨팅 능력을 가진 컴퓨터에서만 학습을 할 수 있고, GPT-2 모델과 같이 1.5B의 파라미터를 가진 모델의 경우는 단일 GPU로는 `fine-tuning` 조차 할 수 없다. 

![](https://miro.medium.com/max/2000/1*tOPx3TSpEF2faZB9_85ArQ.png)
위 그림에서 3가지 색이 다른 안경을 통해 트랜스 포머가 가진 이슈들을 설명한다.
### 문제1. 빨간 안경 - 어텐션 계산
길이 $L$을가진 문장의 어텐션을 계산할 때, $O(L^2)$의 메모리와 시간 복잡도를 가진다.
### 문제2. 검은 안경 - 많은 수의 레이어
N개의 레이어는 N배 많은 메모리를 사용한다. 그리고 각각의 레이어는 역전파 계산을 위해 그 값들을 저장해둔다.
### 문제3. 녹색 안경 - 피드포워드 레이어의 깊이
피드포워드레이어가 어텐션의 액티베이션 깊이보다 더 클 수 있다. 

## Reformer에서의 해결
리포머 모델은 트랜스포머를 개선하여, 단일 가속기와 16GB 메모리를 이용해서 백만 단어에 이르는 context window를 다룰 수 있다.

# Reference
[Illustrating the Reformer](https://towardsdatascience.com/illustrating-the-reformer-393575ac6ba0)
***
# 2. Reformer LSH(Locality sensitive hashing)
> [Illustrating the Reformer](https://towardsdatascience.com/illustrating-the-reformer-393575ac6ba0)를 보며 정리.

## 어텐션과 근접 이웃(attention and nearest neighbors)
![](https://miro.medium.com/max/1400/1*ZWO5_viVU1nPt5bwkAXrXQ.png) 
트랜스포머 모델에서는 위와 같이 3종류의 어텐션이 있다. 어텐션의 과정을 그림으로 보면 아래와 같다.
![](https://miro.medium.com/max/1400/1*gP3LvhmH9fV5qpAPfy4H0w.png)
이때 우측에 `it`의 어텐션을 모습을 보면 5개를 제외하면, 어텐션을 받지 못했는데, 이때 나머지 `didn't`,`cross` 등과 같은 단어들은 어텐션을 받지 않아, 실제로 행렬의 모습은 sparse 하게 된다.  
  
따라서 우리는 쿼리 $Q$에 대해 밀접한 연관을 가진 $K$에 대해서만 어텐션을 하면 된다. 하지만 기존 트랜스포머의 구조는 이부분을 비효율적으로 찾고, 이 부분을 리포머에서 개선한다.  
  
리포머에서는 Dot-Product 어텐션을 *locality-sensitive hasing(LSH)*로 대체하면서 $O(L^2)$를 $O(Llog(L))$로 개선했다. 

## LSH 소개
LSH는 고차원 데이터에 대해 *nearest neighbor* 알고리즘을 효율적으로 근사하는 방법으로 알려져있고, 두 점 `p`, `q`가 충분히 가깝다면 해시 함수를 거친 결과가 hash(p) == hash(q)으로 가정한다.
  
![](https://miro.medium.com/max/1392/1*fN4ck7Jd0gDilFeAZhowpA.gif)


# Reference
[Illustrating the Reformer](https://towardsdatascience.com/illustrating-the-reformer-393575ac6ba0)