# zsh 설정
***
## 1. oh-my-zsh 프롬프트에 기본으로 표시되는 사용자 이름 삭제하기
:기본으로 표시되는 사용자 이름이 자리를 차지해서 불편
```
prompt_context() {
  if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
    prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"
  fi
}
```
위와 같이 수정 후 __source ~/.zshrc__ 으로 적용