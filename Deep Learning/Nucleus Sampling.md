# Nucleus Sampling

> [How to sample from language models](https://towardsdatascience.com/how-to-sample-from-language-models-682bceb97277) 을 보며 정리

![](https://miro.medium.com/max/1400/1*9sEpLZF8lV5OXwUQUMVZlg.png)
  
GPT-2로 텍스트를 생성하다보면, 랜덤 샘플링이나 Top-k 샘플링 등을 사용해도 문맥이 잘 맞지 않는다고 생각이 된다. 추가로 다른 방법 중 `Top-p`, `Nucleus 샘플링`을 찾을 수 있다.  
  
위 참조한 포스트는 *The Curious Case of Neural Text Degeneration by Holtzman et al 2019.*을 정리한 포스트이다.  
  
샘플링 방법중 가장 대중적인 방법은 **temperature** and **top-k** 샘플링이 있다.

## 1. Temperature sampling 
통계 역학에서 영향을 받은 방법으로, 높은 온도(Temperature)는 낮은 에너지 상태가 발생할 가능성이 높다는 것을 의미한다. 확률 모델에서 로짓(logit)은 에너지를 의미하고, 소프트맥스로 로짓을 입력하기 전에 높은 온도(Temperature)에 따라 로짓을 나누면서 `Temperature sampling`을 수행한다. 그 후 샘플링된 확률값들을 얻을 수 있다.
```python
import torch
import torch.nn.functional as F

a = torch.tensor([1,2,3,4])
F.softmax(a, dim=0) # tensor([0.0321, 0.0871, 0.2369, 0.6439])
F.softmax(a/.5, dim=0) # tensor([0.0021, 0.0158, 0.1171, 0.8650])
F.softmax(a/1.5, dim=0) # tensor([0.0708, 0.1378, 0.2685, 0.5229])
F.softmax(a/1e-6, dim=0) # tensor([0., 0., 0., 1.])
```
![](https://miro.medium.com/max/750/0*pgyestIdYz0aNzX0)**그림 1**  
  
Temp가 낮으면 상위 선택들에 대한 신뢰도는 높아지고, Temp가 1보다 높은 경우 신뢰도가 떨어지게 된다. 반면에 Temp가 1보다 더 큰 경우에는 신뢰도를 떨어뜨린다. 0 Temp에서는 argmax/max 우도와 동일한 반면, 제한없는 Temp는 균일한 샘플링에 해당한다.

## 2. Top K 샘플링 단점
![](https://miro.medium.com/max/1400/0*J37qonVPJvKZpzv2)
샘플링의 경우 경우에 따라서 선택할 수 있는 단어의 폭이 다르다.

## 3. Top P 샘플링 aka. Nucleus Sampling
위 단점을 해결하기 위해 `Top p` 샘플링이 제안 되었다. 누적분포를 계산하고, CDF가 P를 초과하면 바로 잘라낸다.  
  
예를들어, top-p = 0.9 일 때, `그림1`에서 위 그림을 보면 고르게 분포된 경우에서는 여러개의 토큰의 분포 값을 합하면 0.9가 될 수 있고, 아래 그림을 보면 'hot'과 'warm'을 합한 것만으로 0.9를 초과할 수 있다. 이런 방법으로 완전히 다른 토큰을 선택하게 되는 문제를 피할 수 있다.

