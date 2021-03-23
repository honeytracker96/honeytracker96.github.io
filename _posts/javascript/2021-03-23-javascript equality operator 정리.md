---
title: javascript(ECMA6) equality operator 정리
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- javascript
description: js equality operator 정리
article_tag1: operator, js, javascript, euqality
meta_keywords: operator, js,javascript, equality
#last_modified_at: '2020-11-21 14:00:00 +08000'
toc: true
toc_sticky: true
toc_label: 목차 
---
# javascript equality operator 정리

javascript를 배우면서 다른 operator의 경우 다른 언어들과 크게 다를게 없어서 짚고 넘어가지 않아도 될 것같지만`(==) equality`와 `(===)strict equality`가 헷갈리기 쉬워서 나름대로 정리를 하고 넘어가려고 합니다.

>[MDN equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Equality)
<br>[MDN strict equality ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality)
<br>아래의 내용들은 해당 문서를 참고 하여 정리하였습니다.

---
## Equality(==)
Equality 연산자는 값을 비교하는 연산자입니다. 그러나 java같은언어와 다르게 값을 비교할 때 값의 타입을 변환 시켜서 비교를 하게 됩니다. 아래의 예제를 보겠습니다.

```js
console.log("Equality--------");
console.log(123 == '123');               //true
console.log(true == 1);                  //true
console.log(undefined == null);          //true
console.log('abc' == new String('abc')); //true
console.log(null == false);              //false
console.log('true' == true);             //false
console.log(true == 2);                  //flase
console.log(true == 1);                  //true
```
서로 다른 타입을 비교 하였을 때 자동으로 값의 타입을 변환 후 비교하는 것을 볼 수 있습니다.

여기서 값의 변환이 일어 날 때 `undefined == null`은 `true`이지만 `null == false`는 `false`인 것과 `true == 2` 는 `false` 이지만 `true == 1` 은 `true`인 것처럼 확실히 알지 않으면 추후에 코드를 이해하는데 어려움이 있을 수 있는 부분인 것같습니다.

### !연산자를 이용한 비교
추가로 ! 연산자를 이용한 비교와 객체와 객체를 비교해서 결과를 보겠습니다. 
```js
// ! 연산자를 이용한 비교
0 == !!null;          // true, look at Logical NOT operator
0 == !!undefined;     // true, look at Logical NOT operator

console.log(null);        //null
console.log(undefined);   //undefined
console.log(!undefined);  //true
console.log(!null);       //true
console.log(!!undefined); //false
console.log(!!null);      //false
```
`console.log()`로 값을 출력해 보면 **!** 연산자를 사용하면 값이 boolean 타입으로 변환 되는 것을 볼 수 있습니다. 그래서 `0 == !! null`를 하게되면 `null`값이 **boolean 값인 false**로 변환 되어 `true`가 되는 것입니다. 

### 객체의 비교
```js
//객체의 비교
const number1 = new Number(3);
const number2 = new Number(3);
number1 == 3;         // true
number1 == number2;   // false
```
객체는 기본적으로 각각의 주소값을 가지기 때문에 `number1 == number2`의 경우 내부의 값이 아니라 객체의 주소값을 비교하게 됩니다. 따라서 `number1 == 3`은 숫자로 형변환 되어 `true`가 되었지만 `number1 == number2`는 `false`가 된 것입니다. 

---
## Strict Equality(===)
Strict Equality의 strict는 "엄격한, 엄밀한" 이런 의미를 가지고 있다. 그래서 그 의미대로 strict equality에서는 일반 equality 자동 형변환이 일어나지 않는다. 따라서 equlity에서는 true로 나오는 값들이 strict equality에서는  false로 나올 수 있다.

```js
// strict equality 에서 다르게 나오는 결과값

console.log("3" === 3);           // false
console.log(true === 1);          // false
console.log(false === 0);         // false
console.log(null === undefined);  // false
```

그러나 **!** 을 사용한 undefined 와 null 연산은 true로 같은 결과를 가진다. === 연산자 이전에 ! 연산자가 우선순위가 더 높은 것 같다.

```js
0 === !!null;          // true
0 === !!undefined;     // true 

// ! 연산 먼저 진행 후 === 연산 진행
```