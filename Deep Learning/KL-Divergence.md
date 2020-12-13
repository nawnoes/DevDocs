# KL-Divergence(Kullback-Leibler divergence)
## 정보이론
- 정보이론은 정보의 양을 측정하는 분야.
- 그 정보를 표현하는 개념이 엔트로피. 
- 정보를 전달하는 단위는 비트
- 정보의량은 불확실성이 커질 수록 많아진다. 
    > 일상적인 예로 동전던지기와 주사위 던지기의 경우, 동전던지기는 2가지 경우, 주사위는 6가지 경우로 주사위가 표현해야할 정보의량이 더 많다. 그리고 주사위가 동전에 비해 불확실성이 더 높다.

## Self-Information
확률 $P$를 가지는 사건이나 메세지 $A$의 정보를 정의하는것.  
어떤 A에 대한 정보는 $I(A) = log(1/p(A)) = -log(p(A))$  
- 확률은 0~1 값으로 위 값은 음수가 나오게 된다.
- 정보량은 양수 값을 가져야 하므로 -를 씌워 양수로 만들어준다. 
- continuos한 random variable의 경우 log의 밑을 e로 사용한다. 

> 확률이 $1/32$를 가지는 사건 또는 메세지의 정보량은 $-log(1/32)$로 5가 되며, 이때 정보의 단위가 비트인 경우 이 메세지를 전달하기 위해 필요한 비트의 수는 5가 된다. 

## 엔트로피
1. Joint Entropy
2. Cross Entropy
3. Conditional Entropy

## KL divergence
cross entropy를  사용해서 분포 $p$, $q$의 유사한 정도를 계산하는 방법. cross entropy는 $p$를 $q$를 설명하는 정보량을 뜻한다. cross entropy에서 p가 자기자신을 설명하는 정보량인 p의 엔트로피의 차이가 KL-Divergence가 된다. 



## References
- https://reniew.github.io/17/
