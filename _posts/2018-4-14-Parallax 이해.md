---
layout: post
title:  "Parallax 이해"
author: "Paritta"
---
 
## 원리

<img src='https://alligator.io/images/react/react-css.png'>
무작정 css로 구현하는 parallax를 찾아서 따라하다보니까 구현하기가 힘들다. 정확하게 어떻게 동작 하는지 알아야 다른 더 복잡한 parallax를 구현하는데 도움이 될 것 같다.

- [100% CSS Parallax Scrolling Effect](https://www.okgrow.com/posts/css-only-parallax)
구글링을 해보면 예제가 좀 있는데 위 글이 제일 나은것 같다.

``` css
.MainContainer {
  perspective: 1px;
  transform-style: preserve-3d;
  height: 100vh;
  overflow-x: hidden;
  overflow-y: scroll;
}
```

위 예제를 인용해서 설명을 하자면...
먼저 Parallax가 동작할 수 있는 환경을 만들어 준다.
transform-style: preserve-3d;를 이용해서 컨테이너 안에 있는 요소가 translateZ를 이용할 수 있게 해준다.
overflow-y만 동작 해야 하기 때문에 x는 hidden 시켜준다.
parallax는 내가 보는 전체 화면에서 동작되기 때문에 height 100vh로 동작 반경을 전체 화면으로 제한시켜준다. 

``` css
.ParallaxContainer {
  display: flex;
  flex: 1 0 auto;
  position: relative;
  height: 100vh;
  transform: translateZ(-1px) scale(2);
  z-index: -1;
}
```

첫번째로 올린 사진에서 이 ParallaxContainer를 중간에 있는 스크린으로 이해하면 된다. z-index가 -1이기 때문에 위에 있는 스크린에 비해서 상대적으로 아래에 위치할 수 있게 된다. 그리고 이 상황을 설명하기 위해서 한 가지 예를 들자면 차를 타고 창 밖을 보는 경우를 생각해 볼 수 있다. 차 안에서 멀리 있는 산을 보면 느리게 움직인다. 멀리 있기 때문에 그렇게 느껴지게 된다. translateZ가 중간에 있는 스크린을 멀리 있는 산처럼 보이게 만들 수 있다. 저 라인 때문에 스크롤을 내렸을때 위에 있는 스크린 보다 상대적으로 느리게 움직이게 되는 것이다. Z축을 이용해서 화면이 작아보이게 만들었기 때문에 어색하게 보이지 않기 위해서 scale을 이용해서 다시 정상 크기로 돌려준다.

``` css
.ContentContainer {
  display: block;
  position: relative;
  background-color: white;
  z-index: 1;
}
```

이 부분은 위에 있는 스크린이다. z-index가 1이기 때문에 위에 위치하게 된다.

- [Performant Parallaxing](https://developers.google.com/web/updates/2016/12/performant-parallaxing)
추가 자료.
