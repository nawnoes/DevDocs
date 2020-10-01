# CS 기술 관련 질문 
아래 내용들에 관한 기술관련 질문 모음
- 기초 CS 
- Java, Python
- React, Spring, nodejs, 

# Question
## Atitute
- 협업할때 어떻게 일하는지
- code 리뷰는 
## Commmon
- Class, Object, Instance의 차이점이 무엇인가요
- Overriding과 Overloading의 차이점은?
- 동기 비동기에 대해 설명하고 각각의 장단점

## OS

## Data Structure & Algorithm
- Quick sort/ Bubble sort 설명과 구현
- 자료구조 스택, 트리, 큐, 힙에 대해 설명

## Network
- 네트워크에서 OSI 7 Layer에 대해 설명

## DB
- DB에서 인덱스에 대해 설명

## Language

## JAVA
- Garbage Collector에 대해 설명
- Single ton 패턴을 사용하는 이유를 
- 스레드의 순서가 보장되는 코드를 짜보시오
- 스프링 사용하는 이유
- JVM 구조

## Python
## React
: Facebook에서 개발하고 관리하는 Javascript 라이브러리. 
- real DOM 과 Virtual Dom 
    + dom(document object model): html 문서를 프로그래밍으로 접근 가능하게 해줌
        * html은 브라우저에 의해 노드 개체들의 트리구조로 변환
        * dom의 목적은 js를 사용해 문서에 대해 프로그래밍 인터페이스를 제공
    + real dom
    + virtual dom
        * 실제 dom에 사본으로 react에서는 real dom과 비교하여 변경부분만 업데이트 할 수 있다.

- react 특징
    + 단방향 데이터 흐름: 부모에서 자식 컴포넌트로 데이터가 단방향으로 흐름
    + Virtual Dom: 가상
    + Component 기반: 컴포넌트 단위로 나누어 재사용성 및 유지보수에 강점
- JSX란
    + JSX는 Javascript XML의 약자
    + JSX는 HTML 
- Flux와 Redux
    + Redux는 react에서 단방향 데이터 흐름이 아닌 하나의 저장소로 부터 관리해줄 수 있게 하는 패턴
        * 특징
            - single source of truth
            - state is read only
            - change are made with pure functions: reducer는 순수함수로 구성되어야 한다.
    + flux 
- 상태가 있는 컴포넌트와 상태가 없는 컴포넌트란?
    + 상태 있는 컴포넌트: 내부적으로 state를 가지고 있고, UI와 관련된, state를 가지고 있어, 상태를 변경할 수 있다.
    + 상태가 없는 컴포넌트: 내부적으로 state가 없어 부모로 부터 받은 props를 이용하는 컴포넌트. 상태를 변경하지 않아 부작용이 없음을 보증

