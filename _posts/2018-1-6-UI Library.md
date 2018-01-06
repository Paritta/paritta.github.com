---
layout: post
title:  "UI Library"
author: "Paritta"
---
 
<img src='https://excodus.com/storage/app/uploads/public/571/646/d5e/571646d5e7bb6046941113.png'>

``` css
/** Pure CSS wave effect **/
div.wave{
	position: absolute;
	left: 0;
	right: 0;
	bottom: 0;
}
div.wave > span{
	display: inline-block;
	width: 10%;
	height: 200px;
	animation: animate 1.5s ease-in-out alternate infinite;
}
div.wave > span:nth-child(1){
	background-color: #B58900;	
}
div.wave > span:nth-child(2){
	background-color: #F7877C;
	animation-delay: .2s;
}
div.wave > span:nth-child(3){
	background-color: #0E7DA8;
	animation-delay: .4s;
}
div.wave > span:nth-child(4){
	background-color: #C4EADF;
	animation-delay: .6s;
}
div.wave > span:nth-child(5){
	background-color: #B4A4CB;
	animation-delay: .8s;
}
div.wave > span:nth-child(6){
	background-color: #FBD92F;
	animation-delay: 1s;
}

// 중략....
```

출처: (https://gist.github.com/minitech/6001839)[https://gist.github.com/minitech/6001839]


순수하게 버튼에 웨이브 효과를 주는 코드라는데 써보진 않았지만 이 정도 길이를 보니 UI 라이브러리를 쓰는게 좋다는 생각이 든다. UI라이브러리 쓸려다 보면 무슨 react 버전을 다운 그레이드 해야하는 상황이나 여러 짜증나는 상황이 많기 때문에 최대한 안쓰는게 좋은 것 같다. 이제 모달 정도는 만들 수 있기 때문에 물론 다음에도 모달은 그냥 땡 자바스크립트, CSS로 만들거다.

어느 회사 면접에서 `Sass`랑 `Styled Components`랑 같이 쓰는 거 어떻게 생각하냐고 물어본적 있는데, 이거랑 비슷한 맥락인가??? 아닌가??? 생각해본 적 없다고 했는데 코드가 보기 싫어지지 않을까... UI 라이브러리랑 그냥 CSS랑 같이 써도 보기 싫을거 같다.