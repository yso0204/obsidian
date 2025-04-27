
App.js에서 TabBar를 수정
```js
    const tabBar = new Tabbar({
        $app,
        initialState: '',
        onClick: async (name) => {
            // 주소에 /panda 같은 값들이 들어가게 수정
            history.pushState(null, `${name} 사진`, name);
            this.setState({
                ...this.state,
                curreneTab: name,
                photos: await request(name === 'all' ? '' : name),
            })
        }
    });
```

popState 추가
`widow`객체의 `addEvenetListner`를 이용, `popState`이벤트는 뒤로 가기, 앞으로 가기 등의 이벤트로 `history api`를 통해 브라우저 