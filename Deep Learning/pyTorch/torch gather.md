# Torch gather 설명
간혹 깃헙을 보다보면 torch gether를 볼수가 있는데 어떻게 동작하는 건지 잘 이해되지 않아 정리해본다.

# torch.gather란 
`input` 텐서가 입력으로 주어지고, 차원 `dim`을 따라서 각 행으로부터 값을 취해, 새로운 텐서를 반환한다.  
  
`torch.LongTensor`를 `index`로 전달하고, 각 행으로부터 값들을 얻는다.`output`텐서의 차원은 `index`텐서의 차원과 같다. 
![](https://i.stack.imgur.com/nudGq.png)
> 주의! 그림에서 인덱싱은 0이 아닌 1부터 시작


그림의 첫번째는 행방향으로 진행 위에서 아래방향으로 진행. 첫번째 행의 value가 1이므로,result에서 (1,1) 위치에 있는 1 을 선택 

`index`행렬에서 $i$ 번째행과 $j$번째 열의 값을 $v$라 할때  
$v = index[i][j]$  
$result[i][j] = src[i][v]$으로 진행된다.

두번째 그림은 열 방향으로 진행
`index`행렬에서 $i$ 번째행과 $j$번째 열의 값을 $v$라 할때  
$v = index[i][j]$  
$result[i][j] = src[i][v]$으로 진행된다.  
  
완전히 이해되지는 않아, 사용해보면서 추가적인 이해가 필요할것으로 보인다.
추가적인 참고는 아래 사이트들을 참고하길 추천.

# References
https://dukeyang.tistory.com/14
https://stackoverflow.com/questions/50999977/what-does-the-gather-function-do-in-pytorch-in-layman-terms