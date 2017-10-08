---
layout: post
title:  "immutable.js를 써야하는 이유"
author: "Paritta"
---
 
<img src='http://blog-assets.risingstack.com/2016/Jan/immutable_logo_for_react_js_best_practices-1453211749818.png'>

# immutable.js를 써야하는 이유

*[http://reactkungfu.com/2015/08/pros-and-cons-of-using-immutability-with-react-js/](http://reactkungfu.com/2015/08/pros-and-cons-of-using-immutability-with-react-js/)*

위 문서를 참고함...

```javascript
var yourCar = {
  color: 'red',
  .. the same as neighboursCar
};

var neighboursCar = {
  color: 'red',
  ... the same as yourCar
};
```

링크에 있는 문서의 예제를 보장.

```javascript
yourCar.color = 'blue'; // reference stays the same!
```

주석에 나와 있는 것처럼 yourCar의 색깔은 바꼈지만 참조는 같다.

> *그럼 yourCar의 참조를 어떻게 바꿔야할까?*

`assign()`함수를 사용하는 상황을 생각해보자. 

```javascript
var yourCarRepainted = Object.assign({}, yourCar, { color: 'blue' });

yourCarRepainted === yourCar; // false
```

새로운 참조를 만드는데 메모리 낭비다...

```javascript
var yourCarRepainted = Object.assign({}, yourCar, { color: 'red' });

yourCarRepainted === yourCar; // false :(
```

위의 예제는 또 색깔은 같지만 ===연산을 해보면 다르다고 나온다.

> *The only problem is mutations that you perform but doesn’t change a value at all also creates a new object:*

문서에서 이런 문제를 위와 같이 소개하고 있다.... 좋은 내용같아서 메모!
