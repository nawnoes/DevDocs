# ReforBERT를 pretrain 과정 정리

## mask_tokens 
입력 문장을 토큰화 후 마스킹 된 input과 label들을 생성한다 .
`torch.bernoulli`를 통해 확률로 True False 결정
```python
masked_indices = torch.bernoulli(probability_matrix).bool()
```

### 80%에 대해 [MASK] 토큰 추가
```py
# 80% of the time, we replace masked input tokens with tokenizer.mask_token ([MASK])
  indices_replaced = torch.bernoulli(torch.full(labels.shape, 0.8)).bool() & masked_indices
  inputs[indices_replaced] = tokenizer.convert_tokens_to_ids(tokenizer.mask_token)
```
## ~torch.tensor
torch.tensor에 대해서 앞에 물결을 붙이는 경우가 있다. 
```python
>>> import torch
>>> a = torch.tensor([1,23, 45,5])
>>> [~a]
Out[4]: [tensor([ -2, -24, -46,  -6])]
```

## @ 연산자 

```python
a = torch.tensor([1,2,3,4,5,6]).view(3,2)
b = torch.tensor([9,8,7,6,5,4]).view(2,3)
ab = torch.matmul(a,b)
ab = a@b # @ 연산자를 이용하여 간단하게 행렬곱을 표현할 수 있음
```

## torch.full(size, value)
size의 모양을 가진 매트릭스를 value로 채운다.
```py
torch.full([3,5],0.5)
Out[7]: 
tensor([[0.5000, 0.5000, 0.5000, 0.5000, 0.5000],
        [0.5000, 0.5000, 0.5000, 0.5000, 0.5000],
        [0.5000, 0.5000, 0.5000, 0.5000, 0.5000]])
```

## torch.bernoulli
베르누이 분포를 생성
```py
a1 = torch.bernoulli(torch.full([1,22],0.5)
#tensor([[0., 0., 0., 0., 0., 0., 1., 1., 1., 1., 0., 0., 1., 1., 1., 0., 0., 0., 1., 1., 0., 1.]])
```

# F.pad
행렬 a에 대해 앞에 n개, 뒤에 m개의 값x인 패딩을 반환
```py
F.pad(a, pad=(n, m), value=x)
```

```py
>>> a
tensor([ 1, 23, 45,  5])
>>> F.pad(a, pad=(1, 5), value=77)
tensor([77,  1, 23, 45,  5, 77, 77, 77, 77, 77])
```
