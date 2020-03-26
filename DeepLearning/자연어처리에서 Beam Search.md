# 자연어처리에서 Beam Search
텍스트 생성 문제에 대해서 **Greedy Searcg**와 **Beam Search**을 어떻게 사용하는지 

# 텍스트 생성을 위한 Decoder
캡션 생성, 요약, 기계 번역은 단어들의 연속을 예측한다. 이런 모델들의 출력은 각 단어들에 대해 사전크기의 확률 분포이다. 이 사전 크기의 확률 분포들은 문장속의 단어로 변환된다.  
  
가장 가능성이 높은 출력 시퀀스를 디코딩하는 것은 그 가능성에 기초하여 가능한 모든 출력 시퀀스를 검색하는 것을 포함한다. 이때 vocab의 크기는 수백 수천, 수백만이 될때가 있다. 따라서 
탐색문제는 출력 시퀀스에 지수적이기 때문에 완전히 탐색하기 어렵다. 그래서 **휴리스틱 탐색** 방법이 사용한다. 휴리스틱은 보다 근사적이거나 충분하게 디코딩된 출력 시퀀스를 반환한다.  
  
단어들의 후보 시퀀스들은 그들의 우도(likelihood)에 따라 점수화 되고, 다음 텍스트를 예측하는 것에 **Greedy Search**와 **Beam Search**을 일반적으로 사용한다.

# 1. Greedy Seaerch Decoder
greedy search는 각 출력을 예측하는데 각 스텝에서 가장 가능성이 높은 단어를 선택한다. 
**장점**  
탐색하는데 매우 빠르다.
**단점**  
최종 출력이 최적화된 결과에서 멀어진다.
  
## 예제
10개의 단어 시퀀스롤 포함하는 예측문제. 각단어는 다섯 단어의 어휘에 대한 확률 분포를 예측한다

**데이터**  
```python
# define a sequence of 10 words over a vocab of 5 words
data = [[0.1, 0.2, 0.3, 0.4, 0.5],
		[0.5, 0.4, 0.3, 0.2, 0.1],
		[0.1, 0.2, 0.3, 0.4, 0.5],
		[0.5, 0.4, 0.3, 0.2, 0.1],
		[0.1, 0.2, 0.3, 0.4, 0.5],
		[0.5, 0.4, 0.3, 0.2, 0.1],
		[0.1, 0.2, 0.3, 0.4, 0.5],
		[0.5, 0.4, 0.3, 0.2, 0.1],
		[0.1, 0.2, 0.3, 0.4, 0.5],
		[0.5, 0.4, 0.3, 0.2, 0.1]]
data = array(data)
```
각 단어들은 정수로 vocab에서 검색 가능하고, 따라서 디코딩 작업은 확률에서 정수 시퀀스를 선택하는 것이 된다.
`argmax()`는 배열에서 최대값을 갖는 인덱스를 반환해주고 numpy 배열에서 사용 가능하다.  
> greedy_decoder()는 `argmax()` 함수를 이용한다

**Greedy Decoder**  
```python
# 그리디 디코더
def greedy_decoder(data):
    # 각 데이터에서 가장 큰 값을 가지는 인덱스들의 배열을 반환
	return [argmax(s) for s in data]
```

**전체 코드**
```python
from numpy import array
from numpy import argmax

# greedy decoder
def greedy_decoder(data):
	# index for largest probability each row
	return [argmax(s) for s in data]

# define a sequence of 10 words over a vocab of 5 words
data = [[0.1, 0.2, 0.3, 0.4, 0.5],
		[0.5, 0.4, 0.3, 0.2, 0.1],
		[0.1, 0.2, 0.3, 0.4, 0.5],
		[0.5, 0.4, 0.3, 0.2, 0.1],
		[0.1, 0.2, 0.3, 0.4, 0.5],
		[0.5, 0.4, 0.3, 0.2, 0.1],
		[0.1, 0.2, 0.3, 0.4, 0.5],
		[0.5, 0.4, 0.3, 0.2, 0.1],
		[0.1, 0.2, 0.3, 0.4, 0.5],
		[0.5, 0.4, 0.3, 0.2, 0.1]]
data = array(data)
# decode sequence
result = greedy_decoder(data)
print(result)
```
**출력**
> [4, 0, 4, 0, 4, 0, 4, 0, 4, 0]



# References
https://machinelearningmastery.com/beam-search-decoder-natural-language-processing/