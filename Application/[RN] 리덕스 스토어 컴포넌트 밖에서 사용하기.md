# React Native 리덕스 스토어 컴포넌트 밖에서 사용하기
리덕스를 사용하다 보면 리덕스 스토어를 컴포넌트 바깥에서 사용해야하는 경우가 필요.

## 사용법

```js
// redux/store/index.js
export function configureStore(){
    const store = createStore(rootReducer,applyMiddleware(ReduxThunk));
    // const persistor = persistStore(store); // persistor는 에러 발생하므로 주석
    return {store}; //, persistor};
}
```

```js
import { configureStore} from  'redux/store';//
const { store} = configureStore() //configureStore(); persist 사용하지 않는경우

hello_user = ()=>{
    const user= store.getState().all.user
    consoel.log('hello ', user)'
}

```

위와 같이 사용. `store.getState().all` 뒤에 리덕스에서 선안한 변수에 접근하여 사용할 수 있다.

# References
[Access the Redux Store Outside a React Component](https://daveceddia.com/access-redux-store-outside-react/)