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

> 위 네가지 부분들을 각각 이해하고 학습하여도 이해하는데 지장 없다. 
> Axial Positional Encoding은 공식 페이퍼에 소개 되지 않았지만, 허깅페이스 블로그에서 그내용을 다룬다.

## 1. 리포머의 셀프 어텐션 레이어
: 리포머는 2개의 셀프 어텐션 레이어를 이용한다. 하나는 `local self-attention`과 `Locality Sensitive Hashing self-attention`레이어를 사용한다.  
  
> 리포머는 causal self-attention을 위해 소개 되었지만 `bi-directional self-attention`에도 잘 동작한다. 이 포스트에서는 `bi-directional self-attention`을 위한 리포머의 셀프 어텐션을 소개한다.


### 1.1 Global Self-Attention
모든 트랜스포머 모델들의 핵심은 **셀프 어텐션** 레이어에 있다. 전통적인 셀프 어텐션 레이어를 여기서는 **Global self-attention** 레이어라 부른다. 
- Embedding Vector: $X = x_1,...,x_n$
- 각 Embedding Vector $x_i$의 크기는 `config.hidden_size`  
  
Global Self-Attention의 경우 Embedding Vector $X$를 **Query** $Q$, **Key** $K$, **Value** $V$로 되고, **output** $Z$를 얻게 된다. 
- $Z= SelfAttention(X)$
- $SelfAttention(X)=softmax(QK^{T})V$
- $Z = softmax(QK^T)V$ 

n=16이고, $d_h$=3일때 그림은 아래와 같다.
![](https://raw.githubusercontent.com/patrickvonplaten/scientific_images/master/reformer_benchmark/conventional_attention.png
)  
이때 $x_{3}$은 결과 값인 $z_{3}$과 대응 된다. 셀프어텐션의 개념은 멀티헤드 셀프 어텐션으로 쉽개 확장될 수 있다.  
  
리포머를 이해하는데 있어서 셀프 어텐션에서 주요하게 짚고 넘너가야할 부분은 $softmax(QK^{T})V$ 에서 $QK^{T}$에서 inner dot-product를 할때 $O(n^2)$의 메모리 복잡도를 가지는데 있다. 이 부분은 트랜스포머 모델에서 메모리 부족을 야기하는 주요한 부분이다. 

### 1.2 Local Self-Attention
로컬 셀프 어텐션은 $O(n^2)$인 메모리 보틀넥을 줄이기 위한 해결책으로 제시되며, 긴 시퀀스를 가진 모델의 계산 비용을 줄이게 해준다. 
- Local Self Attention Input $X=X_{1:n}=x_1,...,x_n$을 $n_c$ chunk들로 자른다 
- $n_c chunks:X=[X_{1:l_c},...,X_{(n_c-1)*l_c:n_c*l_c}]$
- $l_c$s는 `config.local_chunk_length`

청크 단위로 잘라진 이후 **global self attention**을 각 청크마다 적용한다. 

#### 나눠지기전 input
n=16, $d_h$ = 3인 $n*d_h$ 행렬을 가진 input $X$
![](https://raw.githubusercontent.com/patrickvonplaten/scientific_images/master/reformer_benchmark/input.png)

#### chunk 단위로 나눠진 후 input과 self-attention
$l_c$ =4, $n_c$ =4 일때, Chunked attention
![](https://raw.githubusercontent.com/patrickvonplaten/scientific_images/master/reformer_benchmark/chunked_attention_1.png)
# References
- https://huggingface.co/blog/reformer
- https://github.com/patrickvonplaten/notebooks/blob/master/PyTorch_Reformer.ipynb
- https://colab.research.google.com/github/patrickvonplaten/blog/blob/master/notebooks/03_reformer.ipynb