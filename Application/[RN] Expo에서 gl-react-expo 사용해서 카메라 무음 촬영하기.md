# Expo에서 gl-react-expo 사용해서 카메라 무음 촬영하기
리액트 네이티브에서 일반 카메라를 사용하는 경우 무조건 셔터 소리가 나게되고, 컨트롤 할 수 있는 부분이 네이티브 단이라, expo에서 컨트롤 할 수 있는 부분이 제한 되게 된다. 그 중 여러가지 방법을 찾다가 [RN으로 인스타 필터 및 편집 유튭](https://youtu.be/AMAJLgafs6U)에서 `gl-react-expo`를 이용해 카메라의 필터를 조절하는 것을 보고, 그 방법에서 무음 카메라 아이디어를 얻어서 구현 하였다.

- gl-react-expo의 깃헙은 [이곳](https://github.com/gre/gl-react/tree/master/packages/gl-react-expo)에서 참조 가능하다.
- gl-react의 Surface를 캡쳐하는 방법은 [이곳](https://stackoverflow.com/questions/39913014/is-it-possible-to-save-effected-image-from-gl-react-native)에서 참조 가능
- gl-react의 문서는 [이곳](https://gl-react-cookbook.surge.sh/)에서 확인 가능

## 필터 변경하는 부분 소스 
```js
        <View style={styles.fields}>
          {fields.map(({ id, ...props }) => (
            <Field
              {...props}
              key={id}
              id={id}
              value={effects[id]}
              onChange={this.onEffectChange}
              onReset={this.onEffectReset}
            />
          ))}
        </View>
```