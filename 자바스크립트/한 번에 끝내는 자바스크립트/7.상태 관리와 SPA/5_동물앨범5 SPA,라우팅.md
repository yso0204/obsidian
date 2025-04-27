
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
`widow`객체의 `addEvenetListner`를 이용, `popState`이벤트는 뒤로 가기, 앞으로 가기 등의 이벤트로 `history api`를 통해 브라우저 히스토리가 변경될 때마다 발생한다.

```js
    window.addEventListener('popstate', () => {
        console.log(window.location.pathname);
        
    })
```

앞,뒤 가기 버튼을 눌렀을 때 이전 페이지의 주소 값이 출력된다.

