# torch.bernoulli
reformer 학습 코드 작성 중 `torch.bernoulli` 부분이 있어 정리.


```
  masked_indices = torch.bernoulli(probability_matrix).bool()

```