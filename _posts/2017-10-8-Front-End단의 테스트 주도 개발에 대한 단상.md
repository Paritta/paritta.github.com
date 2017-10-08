---
layout: post
title:  "Front-End단의 테스트 주도 개발에 대한 단상"
author: "Paritta"
---
 
<img src='https://cdn-images-1.medium.com/max/1362/1*9OxlTTIo8K3M82iQPbW03g.png'>

테스트 주도 개발을 할때는 먼저 테스트 코드를 작성하는게 중요하다고 알고있다.
어떤 개발자의 디버깅 시간이 70프로 개발시간이 30프로라고 하자. 이 비율은 개발자가 오류가 발생했을때 오류를 전체 코드에서 찾기 때문이라고 생각한다. 하지만 먼저 테스트 코드를 작성하면 지금 짜고 있는 로직에 대해서만 집중할 수 있기 때문에 저 비율이 50프로, 50프로 정도로 디버깅 시간을 줄일 수 있다. 아니면 디버깅 비율이 더 낮아질 수도 있다. 아직 테스트에 대해서 공부하고 있기 때문에 이런 생각에는 자신이 없다. 테스팅도 양이 방대해서 공부를 많이 해야될 것 같다...

프론트 엔드 개발의 경우에는, 다음과 같은 예제를 찾고하자.

```javascript 
describe('Header', () => {
    it('should render correctly', () => {
      const { output } = setup();

      expect(output.type).toBe('header');
      expect(output.props.className).toBe('header');

      let [h1, input] = output.props.children;

      expect(h1.type).toBe('h1');
      expect(h1.props.children).toBe('todos');

      expect(input.type).toBe(TodoTextInput);
      expect(input.props.newTodo).toBe(true);
      expect(input.props.placeholder).toBe('What needs to be done?');
    });
```

*[https://deminoth.github.io/redux/recipes/WritingTests.html](https://deminoth.github.io/redux/recipes/WritingTests.html)*

위 문서에서 참고한 내용이다.
이 테스트 코드를 보고 이게 에러를 찾기 위한 과정이라고 볼 수 있을까?라는 생각이 든다.
저기서 h1하나가 제대로 작동하지 않아서 글자가 브라우저에서 `<p/>`태그처럼 표현된다고 해서 이 경우에도 자바스크립트 코드를 디버깅할 때처럼 디버깅 시간이 많이 걸릴까?하는 의문이든다.

결론은 다음과 같은 코드에서는 테스트 주도 개발처럼 굳이 테스트 코드를 먼저 짜고 코드를 짜는 일을 하지 않아도 될 것 같다.
