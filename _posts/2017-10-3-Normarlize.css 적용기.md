---
layout: post
title:  "Normarlize.css 적용기"
author: "Paritta"
---

<img src='http://kendsnyder.com/wp-content/uploads/2016/04/post-41282490.jpeg'>

# Normarlize.css 적용기

*[https://github.com/necolas/normalize.css/](https://github.com/necolas/normalize.css/)*

요 문서를 보고 어떻게 적용하는지 알지?
사용 하는법을 찾기 위해서 구글링을 했다. 그리고 webpack css-loader, style-loader를 적용하고 inedex.js 파일에서 `import normalize.css`했다.
저런 문서를 보고 어떻게 쓰는지 모르면 내가 바본가 싶고 자괴감이 느껴진다....... 나 같은 사람 또 없으세요???...

<img src="../img/Normarlize.css 적용기/스크린샷 2017-10-03 오후 8.15.23.png">

![Image]('{{site.url}}/assets/Normarlize.css 적용하기/1.png')

테두리에 여백이 생기는 문제는 없어졌는데 헤더 위에 여백에 또 생긴걸 볼 수 있다. 크롬 브라우저로 디버깅 해봐도 딱히 문제는 보이지 않는다. 역시 구글링을 해본다.

*[https://stackoverflow.com/questions/7374657/normalize-css-top-header-gap](https://stackoverflow.com/questions/7374657/normalize-css-top-header-gap)*

역시 스택 오버 플로우가 짱이다.

> What you see is `margin collapsing`. When an element with a margin is inside an element without border or padding, the margin collapses with the margin of the parent element. It's the margin of the h1 element that you see at the top. As none of the parents have border or padding, the margin collapses all the way out to the outermost container.

여기서 문제되는 상황이 `margin collapsing`이라는 걸 알 수 있다. 스택 오버 플로우 댓글에

> Thanks for the tip!!! h1, h2, h3, h4, h5, h6{margin:0;padding:0} solve the problem, for the moment. Is there any another way to solve these collapses without affecting margin on headings (h1,h2 ...)? – birkof Sep 10 '11 at 21:09 

를 보고

```css
h1 {
    margin: 0;
    padding: 0;

    display: flex;
    align-items: center;
    justify-content: center;
  }
```
해준다 ㅎㅎ...

<img src="../img/Normarlize.css 적용기/스크린샷 2017-10-03 오후 8.27.11.png">

헤더 위에 여백은 사라졌지만 flex가 적용이 안된게 보인다. flex를 h1태그 안으로 옮겼더니 좌우 센터링은 적용이 됐지만 아래 위로는 센터링이 적용이 안된다. css 트릭을 이용해서 밑으로 땡겨야될 것 같다. ㅎㅎ

*[https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)*

margin collapse에 대한 내용은 위 문서를 참고하자 ㅎㅎㅎ

`부모 및 맏이/막내 요소` 케이스에서 `블록의 top 및 bottom 마진은 때로는 (결합되는 마진 중 크기가) 가장 큰 한 마진으로 결합(combine, 상쇄(collapsed))됩니다,`가 된것 같은데 가장 큰 마진이 normalize.css파일 어디 있는거지???


