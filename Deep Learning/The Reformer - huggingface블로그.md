# 허깅페이스 블로그 The Reformer 정리하기
## 개요
Reformer는 2020년에 소개된 transformer를 메모리 효율적으로 개선한 모델이다.  

그리고 최근 긴 시퀀스의 모델링에 대한 관심이 증가하고 있고, 올해만 해도  `longformer`, `Linformer`, `Sparse Sinkhorn Attention` 와 같은 방법들이 소개 되었다. 이런 긴 시퀀스를 처리할 수 있는 언어 모델에 대한 필요성은 요약, 질의응답 등과 같은 NLP 태스트 들에서 더 긴 입력을 필요로 하게 되기 때문이다. 예를 들어 BERT 모델은 512개의 토큰만 처리 할 수 있는데, 그 보다 더 긴 문장들에 대한 처리도 필요하기 때문이다. `Longformer`와 같은 긴 시퀀스를 모델들은 메모리 오버플로우를 위해 input 시퀀스를 자르지 않아도 되기 때문에 버트 같은 모델들을 뛰어넘는 성능을 가진다.  
  
리포머는 기존의 `bert-base-uncased` 모델에서 512 토큰만 사용했던것과 비교해서 [리포머 데모](https://github.com/patrickvonplaten/notebooks/blob/master/PyTorch_Reformer.ipynb)에서 50만 토큰까지 처리 할수 있는것 까지 보인다.  

리포머는 메모리 사용량을 최소화하기 위해 기본 트랜스포머 모델의 성능을 크게 저하시키지 않으면서 각부분을 개선했다.  
  
### 리포머의 4가지 특징
1. Reformer Self-Attention Layer: 컨텍스트들을 최대한 유지하면서 Self-Attention를 효율적으로 구현
2. Chunked Feed Forward Layers: 큰 Feed Forward Layer들이 가진 시간과 메모리 트레이드 오프 관계를 개선
3. Reversible Residual Layers: residual network의 메모리를 획기적으로 개선
4. Axial Positional Encodings: 매우 긴 길이의 시퀀스에 대해서도 잘 동작하는 Positional Encoding

> 위 네가지 부분들을 느슨하게 연결되어 있어서, 각각 이해하고 학습하여도 지장이 없다. 


# References
- https://huggingface.co/blog/reformer
- https://github.com/patrickvonplaten/notebooks/blob/master/PyTorch_Reformer.ipynb
- https://colab.research.google.com/github/patrickvonplaten/blog/blob/master/notebooks/03_reformer.ipynb