---
layout: single
title: "[Js] 알아두면 편리한 연산자와 표현식"
categories: "Programming"
tag: ["javascript"]
typora-root-url: ../
---

<br />
# 개요 ✏️
<br />
<code>javascript</code>로는 다양한 연산자와 표현식을 사용해서 변수를 사용할 수 있다. 나같은 경우에는 실제 개발하다보면 익숙한 문법 위주로만 쓰게 된다. 개념을 정리할겸 해서, 평소에 알고있던 내용 + 알아두면 유용한 문법을 정리해보았다. 
<br />
# 1️⃣  데이터 병합(merge)
```javascript
// 변수 선언
const array1 = [1, 2, 3];
const array2 = [4, 5, 6];
const people1 = { name : "hodo", age : 30 };
const people2 = { hobby : "soccer", age : 31 };
```
## 배열 병합
```javascript
// 01. concat : array 병합가능 
const solution1 = array1.concat(array2);
console.log(solution1); // [1, 2, 3, 4, 5, 6];
```
## 객체 병합
```javascript
// 02. Object.assign : object 병합가능 
// 키값 중복시 나중에 선언된 객체 우선으로 병합 
const solution2 = Object.assign({}, people1, people2);
console.log(solution2); // { name : "hodo", age : 31,  hobby: "soccer" };
```
## 배열 && 객체 병합
```javascript
// 03. 스프레드 연산자(spread operator) : object, array 두가지 다 병합가능
const solution3 = [ ...array1, array2 ];
const solution4 = { ...people1, ...people2 };
console.log(solution3); // [1, 2, 3, 4, 5, 6]
console.log(solution4); // { name: "hodo", age: 31, hobby: "soccer" }
```
<br />
# 2️⃣  구조 분해
```javascript
// 변수 선언
const person = { name: 'John', age: 30 }; 
const numbers = [1, 2, 3]; 
```
## 객체 구조 분해 
```javascript
const { name, age } = person; // 기본 사용법
console.log(name); // 'John'
console.log(age);  // 30
```
```javascript
const { name : userName, age : userAge } = person; // 키값 별칭 사용
console.log(userName);  // John
console.log(userAge);  // 30
```
```javascript
const { hobby = 'soccer' } = person; // 키값 없을시 기본값 설정
console.log(hobby);  // soccer
```
## 배열 구조 분해 
```javascript
const [a, b, c] = numbers;  // 기본 사용법
console.log(a); // 1
console.log(b); // 2
console.log(c); // 3
```
```javascript
const [a, b, c, d = 4] = numbers; // 원소 없을시 기본값 설정
console.log(d) // 4
```
<br />
# 3️⃣  연산자
```javascript
// 변수 선언
const people = { name : "hodo", age : 30 }
const cars = [ "Bentley", "BMW", "Benz" ]
```
```javascript
// in 연산자: 요소 있을시 true 없을시 false
console.log(hoby in people) // false;
console.log(name in people) // true;
console.log(3 in cars) // false;
console.log(0 in cars) // true;
```
```javascript
// 삼항 연산자 : ? 이전 연산이 true 일시 ? 값, 아닐시 : 값 반영
const inspection1 = people.age > 30 ? true : false;
const inspection2 = cars[2] === "Benz" ? true : false;
console.log(inspection1); // false;
console.log(inspection2); // true;
```
```javascript
// 널 병합 연산자 : 왼쪽값이 null 또는 undefined 일때 오른쪽 값, 그렇지 않을시 왼쪽 값 반환
const todayCar = cars[3] ?? cars[2]
console.log(todayCar); // "Benz"
```
<br />
# 4️⃣  옵셔널 체이닝
옵셔널 체이닝은 프로퍼티에 메서드에 연속적으로 접근하거나 호출할 때, 중간에 <code>null</code> or <code>undefined</code> 일 수 있는 상황에서 예외를 방지하고자 사용된다. 
```javascript
// 변수 선언
const person = {
    name: "hodo",
    address: {
        city: "New York",
        postalCode: "10001"
    }
};
const hobbies = ["soccer", "basketball"]
```
```javascript
const userCity = person?.address?.city;
const userCountry = person?.address?.country;
console.log(userCity) // New York
console.log(userCountry) // undefined
console.log(hobbies[1]?.toUpperCase()) // BASKETBALL
console.log(hobbies[2]?.toUpperCase()) // undefined
```
```javascript
// 널병합 연산자와 함께 사용
const defaultCountry = person?.address?.country ?? 'USA'; 
const defaultTxt = hobbies[2]?.toUpperCase() ?? '요소 범위 벗어남';
console.log(defaultCountry) // USA
console.log(defaultTxt) // 요소 범위 벗어남
```
