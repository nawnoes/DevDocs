# React Native 그림자 효과 주기

## 플랫폼 별로 다른 설정
**설정부분**  
```js
...Platform.select({ 
ios: { 
shadowColor: '#4d4d4d', 
shadowOffset: { width: 8, height: 8, }, 
shadowOpacity: 0.3, shadowRadius: 4, 
}, 
android: { elevation: 8, }, 
}), 
```

### **적용부분**  
**변경 전**  
```js
buttonContainer: {
    backgroundColor: '#272727',
    paddingVertical: 15,
    margin: 10,
    height: 45,
    borderRadius:22,
    width: 350
  },
```
**변경 후**  
```js
buttonContainer: {
    backgroundColor: '#272727',
    paddingVertical: 15,
    margin: 10,
    height: 45,
    borderRadius:22,
    width: 350,
    ...Platform.select({ 
      ios: { 
        shadowColor: '#4d4d4d', 
        shadowOffset: { width: 8, height: 8, }, 
        shadowOpacity: 0.3, shadowRadius: 4, 
      }, 
      android: { elevation: 8, }, 
    }), 
  },
```

## 주의!
부모 컴포넌트에서 `margin`, `padding` 속성을 사용하는 경우 오류가 발생할 수 있다.

# References
- https://honeystorage.tistory.com/164