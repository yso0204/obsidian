
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

이를 `this.updateContent`라는 함수로 묶어서 정리하면
```js
    this.state = {
        // curreneTab: 'all',
        curreneTab: window.location.pathname.replace('/','') || 'all',
        photos:[],
    }

    const tabBar = new Tabbar({
        $app,
        initialState: '',
        onClick: async (name) => {
            // 주소에 /panda 같은 값들이 들어가게 수정
            history.pushState(null, `${name} 사진`, name);
            this.updateContent(name);
        }
    });

    const content = new Content({
        $app,
        initialState: [],
    });
    
    //상태 업데이트
    this.setState = (newState) => {
        this.state = newState;
        tabBar.setState(this.state.curreneTab);
        content.setState(this.state.photos);
    }

    this.updateContent = async (tabName) => {
        const curreneTab = tabName === 'all' ? '' : tabName;
        const photos = await request(curreneTab);
        this.setState({
            ...this.state,
            curreneTab: tabName,
            photos: photos,
        });
    };
    //앞,뒤로 가기 이벤트 발생 시
    window.addEventListener('popstate', async () => {
        this.updateContent(window.location.pathname.replace('/', '') || 'all');
        
    })

    const init = async () => {
        try {
            this.updateContent(window.location.pathname.replace('/', '') || 'all');
        }
        catch (error) {
            console.log(error);
        }
    };

    init();
}
```

하지만 이렇게 해도 아직도 새로고침하면 에러가 뜨는데, 서버가 `/panda`같은 실제 파일이나 라우트를 모르기 때문이다.

지금 `App.js`에서는 `history.pushState()`로 url만 `127.0.0.1/panda` 같은 형태로 바꿔준다.
이건 브라우저 주소창에서만 바뀌고 실제 서버(local host) 는 `/panda`같은 경로를 인식하지 못한다.

즉 사용자가 새로고침하면 브라우저는 서버에 `/panda`같은 경로가 있는지 요청하는데, 하지만 `localhost/src/index.html`만 있고, 해당 경로의 파일은 존재하지 않기 때문에 서버에서 `404` 에러를 띄운다.

그렇기에 SPA 구조에서는 서버가 특정 경로에 대한 요청을 받았을 때, 항상 `index.html`을 반환하도록 설정해주어야 어떤 코드가 들어오더라도 `index.html`을 읽고 정상적으로 `App.js`가 실행될 수 있다.

하지만, vsCode의 extension liveserver는 이러한 기능을 지원하지 않으므로 `node.js`와 `express.js` 같은 서버 사이드 기술을 사용하여 구성해야 한다.
