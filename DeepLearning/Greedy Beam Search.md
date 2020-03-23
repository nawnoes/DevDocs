# Greedy Beam Search

## 트리탐색 구조에서 핵심
모든 경우의 수를 탐색을 바탕으로 하되, 그 가짓수를 하나씩 제거해가면서 정답 트리구조로 나아가는것

## Greedy Search
트리 탐색에서 시작은 탐욕적인 탐색이라 할 수 있을것 

## Beam Search
- 최고우선탐색(Best-First Search) 기법을 기본으로 하되, 기억해야하는 노드 수를 제한하는 방식으로 효율성을 높임.  
- 기억해야하는 노드의 수를 Beam으로 정한다.

### Top-Down
- i번째 step에서 다음 step에 선택될 수 있는 가능한 모든 경우의 수 계산후 최상위 3개 결과만 취해서 i+1 번째 step 결과물로 반환하는 형식.

### Bottom-Up
: 파싱 같은 자연어처리 분야에서는 Bottom-Up Beam Search 기법이 더 많이 사용된다 한다.
- 하위 노드에서 상위 노드로 결합해 나가는 방식



### Top-Down Beam Search
tkddnl 
# References 
https://ratsgo.github.io/deep%20learning/2017/06/26/beamsearch/