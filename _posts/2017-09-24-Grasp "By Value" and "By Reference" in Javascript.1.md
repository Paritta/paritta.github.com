---
layout: post
title:  "Grasp By Value and By Reference in Javascript"
author: "Paritta"
---

# Grasp "By Value" and "By Reference" in Javascript(번역 중)
원문: https://hackernoon.com/grasp-by-value-and-by-reference-in-javascript-7ed75efa1293

자바스크립트는 객체지향 언어다: 이것은 자바스크립트의 대부분이 객체라는걸 의미한다.
예를 들어서, 함수도 객체다. 객체가 아닌 유일한 요소에는 Primitive Da중ta Types : string, number, boolean, null, and undefined 등이 있다
Primitive Data Types는 immutable이다. immutable은 수정될 수 없다는 것을 의미다.

객체는  Value 를 전달 받고 Primitive는 참조를 전달 받는다. ###

> Primitive Data Types are passed By Value and Objects are passed By Reference.

- By Value는 원본의 복사본을 생성한다. ###
- By Reference는 원본에 별칭을 붙이는 것이다. 

Primitive 와 Object가 동작하는 방식을 보자. 먼저 함수의 인자로 값을 할당할 때, = operator로 (=) 할당한다.

## 1.  Assigning a value with the = operator to Primitives an Objects
### Primitive Data Types의 경우 =는 by value 방식으로 동작한다.
코드를 보자.

``` javascript
var name = "Carlos";
var firstName = name;
name = "Carla";
console.log(name); // "Carla"
console.log(firstName); // "Carlos"
```

무슨 일이 일어나는지 정리해보자.

- 변수 `name`를 만들고 "Carlos"를 받는다. 자바스크립트는 변수에 대한 메모리 공간을 할당한다.
- 변수 `firstName`을 만들고 name 복사값을 할당한다. 이 시점에서 `firstName`과 `name`의 메모리 공간은 독립적으로 존재한다. `first의Name`에도 "Carlos"의 값이 존재한다.
- 그리고 `Name`의 값을 "Carla"로 바꾸어도 `firstName`의 값은 다른 메모리 공간에 존재하기 때문에 값이 변하지 않는다.

> When working with primitives, the =operator creates a copy of the original variable. That’s what by value means.

## Objects의 경우 =는 by reference 방식으로 동작한다.

``` javascript
var myName = {
  firstName: "Carlos"
};
var identity = myName;
myName.firstName = "Carla";
console.log(myName.firstName); // "Carla"
console.log(identity.firstName); // "Carla"
```

로그에서 똑같은 값을 출력한다. 왜냐하면, objects의 경우, =가 by reference 방식으로 동작하기 때문이다.
다음을 보자.

- 변수 `myName`을 만들고 `firstName`속성을 가진 객체 값을 받는다. `firstname`은 "Carlos"다.
- 변수 `identity`는 `myName`을 가리킨다.  `identity`에는 메모리 공간이 주어지지 않는다. 그냥 `myName`을 가리킨다.
- `myName`의 `firstName`을 "Carlos"에서 "Carla"로 바꾼다.

`myName.firstName`의 로그를 찍어보면 새로운 값이 나온다. `identity.firtName` 또 `myName.first` 역시 "Carla"를 찍는다. `identity.firtName`가 `myName.firstName`의 메모리 공간을 가리키기 때문이다.

> When working with objects, the =operator creates an alias to the original object, it doesn’t create a new object. That’s what “by reference” means.

## 2. 함수에 Primitives와 Objects를 전달하기.

Primitive Data Types은 by value 방식으로 전달된다.
함수에서 Primitive Data Type을 바꾸면, outer scope에 영향을 주지 않는다.

``` javascript
var myName = "Carlos";
function myNameIs(aName){
  aName = "Carla";
}
myNameIs(myName);
console.log(myName); // "Carlos"
```  

함수를 호출하 출력 할 때, 함수의 `myName`을 바꾸지만 값은 로그는 여전히 "Carlos"다. 왜냐하면 primitive types를 전달할 때, by Value 방식으로 전달되기 때문이다.

함수 내부에서 myName을 어떻게 하든 global scope에 있는 myName에 영향을 주지 않는다.
`myName`의 복사값을 전달했기 때문이다.

### 객체는 함수에 by reference 방식으로 전달된다.
썸씽을 by reference 방식으로 전달 할때, 썸씽을 가리키는 썸씽을 전달한다. 그래서 자바스크립트는 objects를 by reference 방식으로 전달하기 때문에, object의 속성값을 함수 내부에서 변경하면, 변경 내용은 outer scope에 반영된다.

``` javascript 
var myName = {};
function myNameIs(aName){
  aName.firstName = "Carla";
}
myNameIs(myName);
console.log(myName); // Object {firstName: "Carla"}
```

`myNameIs` 함수를 호출하고 `myName`의 로그를 찍어보면 로그는 `firstName`의 키를 가지고, "Carla"값을 가진 object를 찍는다. 

객체를 함수에 전달할 때, 객체는 global scope에 영역에 있는 값도 바뀌게 된다.
왜냐하면 함수에 객체를 전달할때 복사값을 전달하성는 것이 아니기 때문이다. 대신 `myName`을 가리키는 썸씽을 전달한다. 그래서 함수의 객체 속을 바꿀때, outer scope에 있는 객체 속성값 또한 바꾸게 된다.

하지만 당신이 신경써야할 미묘한 부분이 있다.

``` javascript
var myName = {
  firstName: "Carla"
};
function myNameIs(aName){
  aName = {
    nickName: "Carlita"
  };
}
myNameIs(myName);
console.log(myName); // Object {firstName: "Carla"}
```




 