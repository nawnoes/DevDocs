# Expo 앱 상태 체크
**AppState** 는 앱이 동작하거나 백그라운드에 있을 때, 상태가 변경 되는것을 알려준다.  
AppState는 의도와 적절한 행동을 결정하는데 종종 사용되어진다, 푸시 알람을 사용할 때.

## App States
- active: foreground에서 동작
- background: background에서 동작
- [ios] inactive 

## Basic Usage
**AppState.currentState**를 통해서 앱 상태를 알 수 있다. 브릿지를 통해서 추출 되기 전엔 currentState가 null이 될것이다.
```js
import React, { Component } from 'react';
import { AppState, Text } from 'react-native';

class AppStateExample extends Component {
  state = {
    appState: AppState.currentState,
  };

  componentDidMount() {
    AppState.addEventListener('change', this._handleAppStateChange);
  }

  componentWillUnmount() {
    AppState.removeEventListener('change', this._handleAppStateChange);
  }

  _handleAppStateChange = nextAppState => {
    if (this.state.appState.match(/inactive|background/) && nextAppState === 'active') {
      console.log('App has come to the foreground!');
    }
    this.setState({ appState: nextAppState });
  };

  render() {
    return Current state is: {this.state.appState};
  }
}
```
# References
- https://docs.expo.io/versions/latest/react-native/appstate/