# torch.topk
예측 값에서 `argmax`가 아닌 `top-k`에 대한 결과 값을 받고 싶을 때 `torch.topk`를 사용해 받을 수 있다.  
사용 예는 References를 참고.


```python
  # values에는 값
  # indexs에는 인덱스 값
  values, indexs = torch.topk(predict, k=k, dim=-1)

```
# References
https://www.programcreek.com/python/example/101209/torch.topk