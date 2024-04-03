---
layout: single
title: "[Js] 자바스크립트 데이터 타입과 메모리 할당"
categories: "Programming"
tag: ["javascript"]
typora-root-url: ../
---

<br />
# 1️⃣ 데이터 타입 
<br />
자바스크립트 데이터는 크게 2가지로 나뉩니다. 기본형(원시) 타입과 참조(Reference) 타입으로 나뉩니다. 기본형에는 `String`, `Number`, `Boolean`, `Null`, `undefined`, `Symbol` 이 있습니다. 참조형에는 `Array`, `Object`, `Function` 와 ES6 부터 추가된 `Map`, `Set`과 같은 데이터는 참조형입니다.
<table class="min-width">
  <thead>
    <tr>
      <th>데이터 타입</th>
      <th>유형</th>
      <th>특징</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>숫자(형Number)</td>
      <td rowspan="6">기본(원시)형</td>
      <td rowspan="6">데이터가 모두 불변값</td>
    </tr>
    <tr>
      <td>문자열(String)</td>
    </tr>
    <tr>
      <td>Boolean</td>
    </tr>
    <tr>
      <td>Null</td>
    </tr>
    <tr>
      <td>undefined</td>
    </tr>
    <tr>
      <td>Symbol</td>
    </tr>
    <tr>
      <td>객체(Object)</td>
      <td rowspan="5">참조형</td>
      <td rowspan="5">기본성질은 가변값이지만, 설정에따라 불변값 활용 가능</td>
    </tr>
        <tr>
      <td>배열(Array)</td>
    </tr>
    <tr>
      <td>함수(Function)</td>
    </tr>
    <tr>
      <td>Map</td>
    </tr>
    <tr>
      <td>Set</td>
    </tr>
  </tbody>
</table>
> 기본형 데이터는 데이터가 모두 불변값. 즉, 변하지 않는값
> {: .notice--info}

저는 위와같은 기본형 데이터의 특징이 잘 와닿지 않았습니다. `null`, `undefined` 와 같은 값은 `js` 내에서 이미 정해져 있는 불변값입니다. 하지만 `String` 이나 `Number`와 같은 값은 변수로 선언해서 얼마든지 변경해서 사용할수 있다고 생각했습니다. 하지만 `js` 에서 `식별자` 와 `변수` 개념을 구분해서 생각할수 있으면 이해가 되실것입니다.
<br />

# 2️⃣ 변수와 식별자

`변수(variable)`와 `식별자(identifier)`은 혼용되어서 사용되기 쉽습니다. 하지만 둘의 의미는 확실히 차이가 있습니다. <mark><u>식별자</u></mark>는 데이터를 식별하기 위해 사용되는 이름, 즉 <mark><u>변수명</u></mark>을 의미합니다. <mark><u>변수</u></mark>는 말그대로 <mark><u>변하는 데이터 자체</u></mark>를 말합니다. 아래의 데이터를 보겠습니다.
<br />

## 원시타입 데이터

```javascript
var a = "변수";
a += "와식별자";
```

`js`를 조금이라도 아시는 분이라면 위의 `a` 변수값이 '변수와식별자' 라는 값을 갖게 된다는것을 알것입니다. 위와 같은 연산이 이루어 질때 메모리 영역의 변화를 보겠습니다.
<br />

<table>
  <tbody>
    <tr>
      <td rowspan="2">식별자 영역</td>
      <td style="background: #F18A8A;">주소</td>
      <td>...</td>
      <td>1002</td>
      <td>1003</td>
      <td>1004</td>
      <td>...</td>
    </tr>
    <tr>
      <td style="background: #F18A8A;">데이터</td>
      <td>...</td>
      <td></td>
      <td>이름 : a, 값 : @5004</td>
      <td></td>
      <td>...</td>
    </tr>
    <tr>
      <td rowspan="2">데이터 영역</td>
      <td style="background: #F18A8A">주소</td>
      <td>...</td>
      <td>5002</td>
      <td>5003</td>
      <td>5004</td>
      <td>...</td>
    </tr>
    <tr>
      <td style="background: #F18A8A">데이터</td>
      <td>...</td>
      <td></td>
      <td>'변수'</td>
      <td>'변수와식별자'</td>
      <td>...</td>
    </tr>
  </tbody>
</table>
위표에서 식별자영역은 `스택(Stack)`, 데이터영역은 `힙(Heap)` 영역이라고 볼수있다. 이를 깊게들어가면 `CS` 지식과 더 관련이 깊으므로, `JS`의 구조이해를 위해 위와같이 표현했습니다. 연산에서 이뤄지는 메모리의 변화는 이렇습니다.
<br />
1. 식별자 영역에 `a` 식별자를 저장합니다. <br />
2. 데이터 영역에서 `변수` 문자 데이터를 찾습니다. <br />
3. 있으면 해당 주소값을 `a` 식별자에 참조하고, 없다면 데이터영역에 새로만듭니다. <br />
4. `a+='와식별자'`와 같이 기존 식별자에 추가할당시, 데이터 영역에서 '변수와식별자' 문자 데이터를 찾습니다<br />
5. 없을시 새로 생성후, 이 주소값을 `a` 식별자에 참조시킵니다.
<br />
<br />
참조형 데이터의 변화를 알아보겠습니다.
<br />

## 참조형 데이터

```javascript
var obj1 = { a: 10, b: 20 };
var obj2 = obj1;

obj2.a = 20;
```

다음과 같이 `Object` 데이터 변수를 선언하고 할당했을때 `obj1`, `obj2` 의 a 값의 변화는 어떻게 될까요 ? 정답은 두 객체의 `a` 속성 모두 20으로 변하게됩니다.

<table>
  <tbody>
    <tr>
      <td rowspan="2">식별자 영역</td>
      <td style="background: #F18A8A;">주소</td>
      <td>1002</td>
      <td>1003</td>
      <td>1004</td>
    </tr>
    <tr>
      <td style="background: #F18A8A;">데이터</td>
      <td>이름 : obj1, 값 : @5003</td>
      <td>이름 : obj2, 값 : @5003</td>
      <td>...</td>
    </tr>
    <tr>
      <td rowspan="2">데이터 영역</td>
      <td style="background: #F18A8A">주소</td>
      <td>5001</td>
      <td>5002</td>
      <td>5003</td>
    </tr>
    <tr>
      <td style="background: #F18A8A">데이터</td>
      <td>10</td>
      <td>20</td>
      <td>@7103 ~ ?</td>
    </tr>
    <tr>
      <td rowspan="2">객체 @5003의 식별자 영역</td>
      <td style="background: #F18A8A">주소</td>
      <td>7103</td>
      <td>7104</td>
      <td>...</td>
    </tr>
    <tr>
      <td style="background: #F18A8A">데이터</td>
      <td>이름:a, 값: @5002</td>
      <td>이름:b, 값: @5002</td>
      <td>...</td>
    </tr>
  </tbody>
</table>
위와같이 식별자 영역에 있는 `obj1`, `obj2` 가 데이터영역에 `@5003` 주소값을 공유하고 있으므로, 속성값이 바뀜에 따라 두 객체값 모두 값이 바뀌게 된다. 이와같은 현상을 `얕은복사` 라고한다. 다음은 `깊은복사`를 알아보겠습니다.

```javascript
var obj1 = { a: 10, b: 20 };
var obj2 = Object.assign({}, obj1);
obj2.a = 20;
```

`obj2`에 빈객체`({})`와 `obj1` 의 값을 병합(merge) 했습니다. 이러면 메모리의 데이터 영역의 새로운 공간에 새 객체가 저장되고 그 주소를 식별자 영역의 `obj2` 위치에 저장합니다. 이렇게 되면 두 객체가 서로 다른 객체데이터 주소값을 바라보므로 `obj2`의 속성을 바꿔도 `obj1`의 속성값에 영향이 가지 않습니다!

<table>
  <tbody>
    <tr>
      <td rowspan="2">식별자 영역</td>
      <td style="background: #F18A8A;">주소</td>
      <td>1002</td>
      <td>1003</td>
      <td>1004</td>
      <td>1005</td>
    </tr>
    <tr>
      <td style="background: #F18A8A;">데이터</td>
      <td>이름 : obj1, 값 : @5003</td>
      <td>이름 : obj2, 값 : @5004</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td rowspan="2">데이터 영역</td>
      <td style="background: #F18A8A">주소</td>
      <td>5001</td>
      <td>5002</td>
      <td>5003</td>
      <td>5004</td>
    </tr>
    <tr>
      <td style="background: #F18A8A">데이터</td>
      <td>10</td>
      <td>20</td>
      <td>@7103 ~ ?</td>
      <td>@7105 ~ ?</td>
    </tr>
    <tr>
      <td rowspan="2">객체 @5003의 식별자 영역</td>
      <td style="background: #F18A8A">주소</td>
      <td>7103</td>
      <td>7104</td>
      <td>7105</td>
      <td>7106</td>
    </tr>
    <tr>
      <td style="background: #F18A8A">데이터</td>
      <td>이름:a, 값: @5001</td>
      <td>이름:b, 값: @5002</td>
      <td>이름:a, 값: @5002</td>
      <td>이름:b, 값: @5002</td>
    </tr>
  </tbody>
</table>
<br />
이 포스팅은 <mark>장재남</mark> 님의 <mark>코어 자바스크립트</mark> 란 책을 읽고 정리해봤습니다.<br />
이책은 프레임워크나 라이브러리 보다는 `javascript` 언어자체의 기초 또는 심화과정을 다뤘습니다. `javascript` 에 대해서 흥미가 있으신분은 한번쯤 읽어보길 추천드립니다.

[정재남, 『코어 자바스크립트』](https://book.interpark.com/product/BookDisplay.do?_method=detail&sc.saNo=001&sc.prdNo=316439749)<br />
<img src="/assets/images/316439749g.jpeg" alt="코어 자바스크립트 표지" style="zoom:80%;" />
