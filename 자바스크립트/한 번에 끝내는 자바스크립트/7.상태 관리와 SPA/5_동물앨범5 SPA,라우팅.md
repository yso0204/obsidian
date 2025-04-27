
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

이제 페이지가 변경될 수 있도록 수정해주면 아래와 같다.
```js
    window.addEventListener('popstate', async () => {
        console.log(window.location.pathname);
        const tabName = window.location.pathname.replace('/', '') || 'all';
        this.setState({
            ...this.state,
            curreneTab: tabName,
            photos: await request(tabName === 'all' ? '' : tabName),
        })
    })

```
현재 페이지를 tabName에 할당하여 `currentTab`과 `photos`를 수정하여 올바르게 페이지가 렌더링 될 수 있도록 수정


하지만, `.../panda` 이런 상태에서 새로 고침하면 에러 페이지가 나오는데 
`Cannot GET /penguin`

이를 위해 `init()`함수와 초기값 `this.state`를 수정
```js
    this.state = {
        // curreneTab: 'all',
        curreneTab: window.location.pathname.replace('/','') || 'all',
        photos:[],
    }

    const init = async () => {
        try {
            const currentTab = this.state.curreneTab;
            const initialPhotos = await request(currentTab === 'all' ? '' : currentTab);
            this.setState({
                ...this.state,
                photos: initialPhotos,
            })
        }
        catch (error) {
            console.log(error);
        }
    };
```

이렇게 해도 아직 