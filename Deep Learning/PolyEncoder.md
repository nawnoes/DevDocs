# Poly Encoder, Architectures and pre-training strategies for fast and accurate multi-sentence scoring

## Poly-encoder
최근에 프리트레이닝된 트랜스포머들을 수 많은 결과들을 보여주고 있습니다. 문장의 쌍을 비교하는데 일반적으로 2가지 방법을 사용합니다. 하나는 두 문장 전체에 Full Attention을 하는 `Cross-encoder`. 다른 하나는 문장을 각각 Encoding 후에 비교하는 `Bi-encoder`가 있습니다. 하지만 Cross-encoder의 경우 실제 서비스 환경에서 사용하기 어려울 만큼 속도가 느리기 때문에 개선하고자 `Poly-encoder`를 제안 했습니다. 폴리 인코더의 경우 4가지 태스크에 대해 실험하였고 모두 SOTA를 달성했습니다. 폴리 인코더의 경우 크로스 인코더보다 빠르고, 바이 인코더 보다 정확한 장점을 가집니다. 

기존에 생성 태스크나 분류 태스크로 챗봇을 만들때, 부정확한 부분이 있었습니다. 이런 부족한 부분을 개선하고자 이루다에서 사요한 poly encoder를 살펴보고 적용해보고자 합니다.

## Cross-encoder와 Bi-encoder
[문장1], [문장2], [문장3], ... 과 같이 여러개의 문장을 비교하고 스코어링을 할때 대표적으로 사용하는 것이 Crosss-encoder와 Bi-encoder가 있습니다. Cross-encoder의 경우 비교하고자 하는 문장 2개를 [문장A]와 [문장B]를 BERT와 같은 모델에 넣어 계산하는 방법입니다. BERT 같은 큰 모델의 경우, 연산하는데 시간이 오래 걸리고, 문장의 수가 늘어나면 늘어날 수록 실제 서비스 환경에서 사용하기 어려운 단점이 있었습니다.

Bi-encoder은 같은 BERT를 사용해 문장의 유사도를 스코어링 할때, 기존에 가지고 있는 문장들을 BERT 같은 모델로 미리 계산 후 저장해 둔다음.  [문장C], [문장D]를 비교하는 방법입니다. 기존에 문장들은 미리 계산해 저장하기 때문에 서비스 상에서 다시 계산하지 않아도 되는 장점을 가집니다.

논문의 저자들은 Poly encoder의 성능을 실험하기 위해, 기존에 위키피디아 데이터와 토론토 Book 데이터와 비교하여, Reddit 데이터를 사용해 pre-training 전략을 사용하고, dialogue, information retrieval 들에 대해서 실험을 진행했습니다. 

Poly-encoder의 경우 추가적으로 학습가능한 어텐션 레이어를 사용해서 보다 전체 입력들의 

# References
- https://github.com/sfzhou5678/PolyEncoder