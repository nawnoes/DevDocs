# nn.CrossEntropyLoss 사용
pytorch에서 Multi-Class에 대한 Loss를 구할때 nn.CrossEntropyLoss를 사용한다. 예전에 텐서플로에서 one-hot으로 라벨을 만들어 사용하였더니 `1d`타입의 target이 들어와야한다는 에러를 출력했다. 

## 사용예
```python

# 입력
x = torch.Tensor([[0.8982, 0.805, 0.6393, 0.9983, 0.5731, 0.0469, 0.556, 0.1476, 0.8404, 0.5544]]) 

# 라벨
y = torch.LongTensor([1]) 

# 크로스 엔트로피 로스
cross_entropy_loss = torch.nn.CrossEntropyLoss()

# 로스 계산
print(cross_entropy_loss(x, y)) # tensor(2.1438)
```

예전에 텐서플로우에서 클래스 분류 하는 경우 `[1]` 라벨에 대해 [0, 1, 0, 0, 0, 0, 0, 0, 0, 0]과 같은 원핫으로 변형하였는데, 토치에서는 편하게 클래스만 넣어주면 로스에서 사용 가능하다.
  


# Reference
http://www.gisdeveloper.co.kr/?p=8668