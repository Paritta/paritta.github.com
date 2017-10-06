---
layout: post
title:  "[React]테스팅 할때 Hoc때문에 생긴 문제"
author: "Paritta"
---

<img src='https://cdn-images-1.medium.com/max/1362/1*9OxlTTIo8K3M82iQPbW03g.png'>

# [React]테스팅 할때 Hoc때문에 생긴 문제

*[http://redux.js.org/docs/recipes/WritingTests.html](http://redux.js.org/docs/recipes/WritingTests.html)*

위 문서를 참고함...

```javascript
import { connect } from 'react-redux'

class App extends Component { /* ... */ }

export default connect(mapStateToProps)(App)
```

예를 들어서 위 코드를 `App` Component라고 하자.

유닛 테스트를 하기 위해서

```javascript
import App from './App'
```

코드를 실행 시키면
`App` Component가 임포트 되는게 아니라 export default가 적용된 connect를 임포트 하기 때문에 엉뚱한... 뭔가가 임포트 된다

그 엉뚱한 뭔가는 참조된 문서 *Connected Components* 섹션 상단에 Dan이 쓴 higher-order components 에세이에 설명 되있다. 에세이에 보면 `function connectToStores(Component, stores, getStateFromStores) {`
 ... 이런식으로 함수가 감싸져 있는걸 볼 수 있다. 에세이를 읽어보자.

위에서 임포트한 무언가의 정체는 우리가 테스트하려고 하는 `App` 컴포넌트가 아니라 ...

*connect함수가 리턴한 wrapper 함수다.*

> *그럼 `App` Component를 임포트 하는 방법은 뭘까???*

```javascript
import { connect } from 'react-redux'

export class App extends Component { /* ... */ }

export default connect(mapStateToProps)(App)
```

위 코드에 나와있는 것 처럼 `class App ...`를 export 해주는 것이다.
이렇게 코드를 바꿔주면

```javascript
// Note the curly braces: grab the named export instead of default export
import { App } from './App'
```

문서에 나와있는 내용 처럼 curly braces를 이용해서 `App` Component를 임포트 할 수 있다.

*[higher-order components](https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750)*

이 글 짱 재밌다 나중에 시간나면 번역 한번 해봐야겠다.


