<img src="https://ifh.cc/g/7LK9Pp.png" style="max-width: 100%" align="center">

### 목차 
- [1 객체 리터럴](#1-객체-리터럴)
- [2 추가된 객체 리터럴의 확장 기능](#5-추가된-객체-리터럴의-확장-기능) 
    - [2-1 프로퍼티 축약 표현](#2-1-프로퍼티-축약-표현)
    - [2-2 계산된 프로퍼티 이름](#2-2-계산된-프로퍼티-이름)
    - [2-3 메서드 축약 표현](#2-3-메서드-축약-표현)


***

<br>

## 1 객체 리터럴

앞서 [객체 타입](https://github.com/jacenam/WIL-archive/blob/main/JavaScript/JavaScript%20Basic%20Concepts/object%20type.md)에서 객체 리터럴에 대해 간단하게 알아보았다. 객체 리터럴은 객체를 생성하는 데 있어 가장 편리한 방식이다. 중괄호(`{}`) 객체 리터럴을 사용하여 중괄호 내에 0개 이상의 프로퍼티를 JS 엔진이 ‘객체’로 인식할 수 있도록  정의(표현)한다. 아래 예제와 같이 중괄호 내에 프로퍼티를 정의하지 않으면 빈 객체가 생성된다
```javascript
var emptyObj = {}; 
  
console.log(emptyObj, typeof emptyObj); // → {} 'object'
```
앞서 [리터럴](https://github.com/jacenam/WIL-archive/blob/main/JavaScript/JavaScript%20Basic%20Concepts/expression%20%26%20statement(feat.%20value%2C%20literal).md#2-리터럴)은 소스코드가 순차적으로 실행되는 시점인 런타임에 JS 엔진에 의해 평가되어 값을 생성한다 했다. 그러나 객체 리터럴의 경우 변수에 값이 할당되는 시점(소스코드가 순차적으로 실행되는 런타임 이후)에 JS 엔진에 의해 해석되어 객체를 생성한다
> **Reminder**
>
> - 식별자(변수, 함수 등)의 실행 시점: 소스코드가 순차적으로 실행되는 시점인 런타임 이전에 실행
>
> - 리터럴 값의 평가 시점: 소스코드가 순차적으로 실행되는 시점인 런타임에 실행
>
> - 값의 할당 시점: 소스코드가 순차적으로 실행되는 시점인 런타임 이후 실행
객체 리터럴의 중괄호는 제어문(`if`문, `for`문, `while`문)에서 코드 블록을 표현하는 중괄호와 다르다는 것에 주의하자. 객체 리터럴은 객체라는 '값'으로 평가되는 표현식이다. 따라서 객체 리터럴을 '닫는다'라는 의미의 닫는 중괄호(`}`) 뒤에는 '문의 종료'를 의미하는 세미콜론(`;`)을 붙여야 한다. [코드 블록(블록문)]()을 의미하는 제어문의 중괄호(`{}`)는 뒤에는 세미콜론을 붙이지 않는 것이 일반적이다
```javascript
// 객체 리터럴
var obj = {
	1: 0, 
	2: 1
}; 

// 제어문
if ( 0 == false ) {
	var user = 'Jace'; 
} 
```
<br>


## 2 추가된 객체 리터럴의 확장 기능
ES6(2015)에서는 더욱 간편하게 객체를 생성할 수 있도록 객체 리터럴의 확장 기능을 제공한다

### 2-1 프로퍼티 축약 표현
앞서 변수에 할당된 값을 참조할 때 저장된 값을 반환하는 것을 변수의 [식별자 참조](https://github.com/jacenam/WIL-archive/blob/main/JavaScript/JavaScript%20Basic%20Concepts/assignment.md#3-값의-할당과-참조)라 했다. 식별자는 새로운 값을 생성하지는 않지만 JS 엔진에 의해 참조된 값으로 평가되기 때문에 식별자 표현식이라고도 부른다
```javascript
var x = 1, y = 2; 

x; // → 1
y; // → 2
```
ES5(2009)에서는 변수(식별자)를 통해 이미 변수에 할당된 값을 프로퍼티 값에 할당할 수 있었다. 변수 `x`, `y`에 각각 숫자 값 `1`, `2`를 할당하였다. 그리고 객체 `obj`의 프로퍼티 키 `x`, `y`에 각각 변수 `x`, `y`의 값을 프로퍼티 값으로 참조하도록 한 것이다
```javascript
var x = 1, y = 2; 

var obj = {
	x: x, 
	y: y 
}; 

console.log(obj); // → { x: 1, y: 2 }
```
ES6에서는 프로퍼티 값으로 변수를 사용하는 경우, 변수(식별자)와 프로퍼티 키가 동일한 이름일 때 프로퍼티 값의 지정을 생략(Property Shorthand)할 수 있다. 이때 프로퍼티 키는 변수 이름으로 동일하게 자동 생성된다 
```javascript
var name = "Jace"; 
var age = 30; 

var user = { 
	name, 
	age
}; 

console.log(user); // → { name: "Jace", age: 30 }
```
### 2.2 계산된 프로퍼티 이름
문자열 또는 문자열로 암묵적 타입 변환될 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 이를 계산된 프로퍼티 이름(Computed Property Name)이라 부른다

ES5에서는 ‘계산된 프로퍼티 이름’의 방식으로 프로퍼티 키를 동적 생성하려면 대괄호(`[]`) 표기법 안에 값을 참조하는 식별자 표현식을 위치시켜 사용해야 한다
```javascript
// 대괄호 프로퍼티 접근 연산자를 활용한 방법
var verify = 'id'; 
var i = 0; 

var user = {}; 

// 대괄호 표기법 안에 값으로 평가될 수 있는 리터럴을 위치시킨다 
user[`${verify}-${++i}`] = i; // i = 0 + 1, i = 1
user[`${verify}-${++i}`] = i; // i = 1 + 1, i = 2
user[`${verify}-${++i}`] = i; // i = 2 + 1, i = 3

console.log(user); // → { id-1: 1, id-2: 2, id-3: 3 }
```
```javascript
// 대괄호 표기법 안에 값으로 평가될 수 있는 리터럴을 위치시키고 프로퍼티 키에 직접적으로 지정하는 방법
var verify = 'id'; 
var i = 0; 

var user = {
	[`${verify}-${++i}`]: i, 
	[`${verify}-${++i}`]: i, 
	[`${verify}-${++i}`]: i
}; 

console.log(user); // → { id-1: 1, id-2: 2, id-3: 3 }
<br>
```
### 2.3 메서드 축약 표현 <span style="color: #F15F3F"> (학습 후 내용 추가할 예정)</span>

<br>
<br>

***
### 참고 
- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)