# BPE, Byte Pair Encoding
기계 학습 단계에서 학습할 단어를 모아둔것을 단어 집합(vocabulary)이라고 한다. 기계가 학습하지 못한 경우의 단어는 OOV(out of vocabulary)라고 하며, UNK(Unknown Token)이라고 한다.  
  
Subword Segmentation은 하나의 단어가 여러가지 내부 단어들의 조함으로 된 것으로 가정하고, 단어를 전처리한다. 언어를 특성에 따라 의미있는 나누는 것이 중요하며, 이 작업을 처리하는 것을 토크나이저라고 한다.  
  
OOV 문제를 완화하는데 사용하는 BPE 알고리즘과 실무에서 사용할 수 있는 토크나이저 구현체인 **SentencePiece**가 있다.  
  
## 1. BPE
BPE는 94년 제안된 단어 압축 알고리즘. 연속적으로 많이 등장한 글자의 쌍을 찾아서 하나의 글자로 병합하는 방식 
```
XdXac
X=ZY
Y=ab
Z=aa
```

# References
- https://wikidocs.net/22592