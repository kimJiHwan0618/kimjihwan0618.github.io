---
layout: single
title: "[정규식] 개념과 활용예제"
categories: "Programming"
tag: ["regex"]
typora-root-url: ../
---

## 정규식 개념

> 정규식이란??
> {: .notice--info}

정규표현식은 프로그래밍에서 문자열을 다룰 때, 일정한 패턴을 찾아내는 형식 언어입니다..
다양한 프로그래밍 언어와 OS에서 정규 표현식을 지원합니다. <code>메타문자</code>와<code>정규문자</code>를 이용해서 정의 할 수 있습니다.
<br />
<br />
정규식을 쓰는 이유는 사실 간단합니다. 프로그래밍을 하다보면, 특정 문자에서 문자열을 찾아내야 할일이 많습니다.
어떠한 단어 한개를 찾아야 하는 상황이 있을수도 있지만, 특정한 패턴을 기준으로 문자를 찾아야 한다면 정규식을 활용하면 훨씬 간결하게 표현할수 있습니다.
<br />

## 정규식 활용예제

> 정규식 관련된 포스팅 글입니다. 정규식을 잘 활용하면 좋은 코드를 만들수 있습니다. 정규식 공부를 추천드립니다.
> {: .notice--info}

다음과 같은 문자열을 가지고 <code>정규식</code> 문자 이후에 나오는 문장을 추출해보겠습니다. 아래는 <code>java</code> 코드로 된 예시입니다.

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class TestCode {
    public static void main(String[] args) {
        String input = "정규식 관련된 포스팅 글입니다. 정규식을 잘 활용하면 좋은 코드를 만들수 있습니다. 정규식 공부를 추천드립니다.";
        String keyword = "정규식"; // 찾을 키워드
        String regex = keyword + "(.*?)\\."; // 정규식 패턴 생성
        Pattern pattern = Pattern.compile(regex); // 패턴 컴파일
        Matcher matcher = pattern.matcher(input); // Matcher 객체 생성
        // 찾은 경우 출력
        while (matcher.find()) {
            String extractedSentence = matcher.group(1).trim();
            System.out.println(extractedSentence);
        }

        if (!matcher.find()) {
            System.out.println("키워드 이후에 나오는 문장이 없습니다.");
        }
    }
};
```

```java
관련된 포스팅 글입니다
잘 활용하면 좋은 코드를 만들수 있습니다
공부를 추천드립니다
키워드 이후에 나오는 문장이 없습니다.
// 키워드 이후에 문장을 출력
```

위에서 쓰인 정규식은 이러합니다.

```java
String regex = keyword + "\\b(.*?)\\.";
```

<code>keyword + </code> : 변수(정규식)뒤에 <br />
<code>(.\*?)</code> : 값n개를 매칭합니다. <br />
<code>\\.</code> : (dot)이 나올때까지 <br />

- 정규식에서 <code>.</code>(dot)은 메타문자로 취급되므로, 문자열로 취급하고 싶으면 앞에 이스케프 문자 <code>\\</code>를 앞에 붙힙니다.

## 패턴 정의 문법

정규식은 어째건 간에 텍스트 즉, 문자열(문장 또는 문서)에서 찾고자 하는 문자나 패턴을 정의하는 것입니다.<br />
그래서 결론적으로 정규식도 문자나 문자열입니다. 그래서 쌍따옴표("")나 이스케이프 문자("\")를 찾고자하는 문자나 패턴 사이에 넣습니다.<br />
정규식은 정규문자와 메타문자로 구성됩니다. 정규문자는 일반적으로 쓰는 문자를 말합니다.<br />
영어의 알파벳이나 한글의 자음/모음, 또는 숫자 같은 것이 되겠습니다. 메타문자는 특별한 의미를 부여한 문자를 말합니다.<br />
아래는 많이쓰이는 정규식 메타 문자와, 특수 문자를 정리해놓은 표입니다.

### 메타 문자(Meta Character)

<br/>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-style="style14" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 8.83721%; text-align: justify;">메타문자</td>
<td style="width: 12.907%; text-align: justify;">기능</td>
<td style="width: 37.558%; text-align: justify;">설명/의미</td>
<td style="width: 12.2094%; text-align: justify;">예시</td>
<td style="width: 28.3721%; text-align: justify;">예시설명</td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;">[ ]</td>
<td style="width: 12.907%; text-align: justify;">문자 클래스<br>(집합)</td>
<td style="width: 37.558%; text-align: justify;">가능한 문자들의 집합을 의미합니다. []안에 있는 한글자 한글자가 찾고자하는 한글자가 될 수 있는 것 입니다. []안에는 결국 문자 하나의 가능한 조건/집합을 정의하게 됩니다.</td>
<td style="width: 12.2094%; text-align: justify;">"[a-m]"</td>
<td style="width: 28.3721%; text-align: justify;">a부터 m중에 하나의 문자</td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;">\</td>
<td style="width: 12.907%; text-align: justify;">백슬래쉬</td>
<td style="width: 37.558%; text-align: justify;">바로 뒤에 오는 한 문자와 합쳐서 특수기호로 사용됩니다.</td>
<td style="width: 12.2094%; text-align: justify;">"\d"</td>
<td style="width: 28.3721%; text-align: justify;">숫자를 나타내는 특수 문자로 숫자 1자리의 모든 수를 의미합니다.</td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;">.</td>
<td style="width: 12.907%; text-align: justify;">문자</td>
<td style="width: 37.558%; text-align: justify;">새줄 문자(개행문자, \n)를 제외한 모든 하나의 문자.</td>
<td style="width: 12.2094%; text-align: justify;">"he..o"</td>
<td style="width: 28.3721%; text-align: justify;">he 다음에 새줄 문자(\n)를 제외한 어떤 문자든 2개가 있고 그뒤에 o가 있는 패턴을 의미합니다.</td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;">^</td>
<td style="width: 12.907%; text-align: justify;">처음</td>
<td style="width: 37.558%; text-align: justify;">^ 다음의 내용으로 시작</td>
<td style="width: 12.2094%; text-align: justify;">"^hello"</td>
<td style="width: 28.3721%; text-align: justify;">시작이 hello인 패턴을 의미합니다.</td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;">$</td>
<td style="width: 12.907%; text-align: justify;">끝</td>
<td style="width: 37.558%; text-align: justify;">$ 전의 내용으로 끝</td>
<td style="width: 12.2094%; text-align: justify;">"planet$"</td>
<td style="width: 28.3721%; text-align: justify;">planet 으로 끝나는 패턴을 의미</td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;">*</td>
<td style="width: 12.907%; text-align: justify;">0회 이상 반복<br>(수량자)</td>
<td style="width: 37.558%; text-align: justify;">* 직전의 정규문자/메타문자가 0회 이상 반복</td>
<td style="width: 12.2094%; text-align: justify;">"he.*o"</td>
<td style="width: 28.3721%; text-align: justify;">.이 0회 이상 반복, 즉 heo, helo, hello, hellllo 모두 패턴 매칭됨</td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;">+</td>
<td style="width: 12.907%; text-align: justify;">1회 이상 반복<br><span style="background-color: #f9f9f9;">(수량자)</span></td>
<td style="width: 37.558%; text-align: justify;"><span style="background-color: #f9f9f9;">+ 직전의 정규문자/메타문자가 1회 이상 반복</span></td>
<td style="width: 12.2094%; text-align: justify;">"he.+o"</td>
<td style="width: 28.3721%; text-align: justify;"><span style="background-color: #f9f9f9;">.이 1회 이상 반복, 즉 helo, hello, hellllo 들이 패턴 매칭됨</span></td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;">?</td>
<td style="width: 12.907%; text-align: justify;">0 또는 1회<br><span style="background-color: #f9f9f9;">(수량자)</span></td>
<td style="width: 37.558%; text-align: justify;"><span style="background-color: #f9f9f9;">? 직전의 정규문자/메타문자가 0 또는 1회 반복</span></td>
<td style="width: 12.2094%; text-align: justify;">"he.?o"</td>
<td style="width: 28.3721%; text-align: justify;"><span style="background-color: #f9f9f9;">.이 0 또는 1회 발생, 즉 heo, helo 들이 패턴 매칭됨(hello는 안됨)</span></td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;">{n, m}</td>
<td style="width: 12.907%; text-align: justify;">지정횟수 반복<br><span style="background-color: #f9f9f9;">(수량자)</span></td>
<td style="width: 37.558%; text-align: justify;">{} 직전의 문자가 n회 이상 m회 이하 반복</td>
<td style="width: 12.2094%; text-align: justify;">"he.{2}o"</td>
<td style="width: 28.3721%; text-align: justify;"><span style="background-color: #f9f9f9;">.이 2회 발생, 즉 hello 만 패턴 매칭됨(heo, helo, helllo는 안됨)</span></td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;"><span style="color: #202122;">¦</span></td>
<td style="width: 12.907%; text-align: justify;">선택</td>
<td style="width: 37.558%; text-align: justify;"><span style="color: #202122;">¦</span> 전에 문자 또는 후에 문자</td>
<td style="width: 12.2094%; text-align: justify;">"true<span style="color: #202122;">¦</span>false"</td>
<td style="width: 28.3721%; text-align: justify;">"true" 또는 "false"의 패턴을 의미</td>
</tr>
<tr>
<td style="width: 8.83721%; text-align: justify;">()</td>
<td style="width: 12.907%; text-align: justify;">그룹</td>
<td style="width: 37.558%; text-align: justify;">그룹으로 묶기, <span style="color: #202122;">여러 식을 하나로 묶을 수 있음</span></td>
<td style="width: 12.2094%; text-align: justify;"><span style="color: #202122;">"a(b¦d)c"</span></td>
<td style="width: 28.3721%; text-align: justify;"><span style="color: #202122;"><span style="color: #202122;">"abc¦adc"와 같은 의미</span></span></td>
</tr>
</tbody>
</table>
수량자와 선택, 그룹을 제외한 메타 문자는 결국 하나의 문자 조건을 나타냅니다.모든 수량자는 {n, m} 방식으로 바꾸어서 정의할 수도 있습니다. <br />
### 특수 기호(Special Character)
하나의 특수 기호를 이용해서 문자, 숫자, 또는 공백을 각각 대신할 수 있습니다. 그리고 문자열의 시작이나 끝, 그리고 단어의 시작이나 끝 등 출현 위치에 대한 규칙을 정할 수 있습니다. <br />
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-style="style14" data-ke-align="alignLeft">
<tbody>
<tr style="height: 40px;">
<td style="width: 7.51163%; height: 40px; text-align: justify;">특수기호</td>
<td style="width: 63.6046%; height: 40px; text-align: justify;">의미</td>
<td style="width: 11.0465%; height: 40px; text-align: justify;">예시</td>
</tr>
<tr style="height: 40px;">
<td style="width: 7.51163%; height: 40px; text-align: justify;">\b</td>
<td style="width: 63.6046%; height: 40px; text-align: justify;">63개 문자(영문 대소문자 52개 + 숫자 10개 + _(underscore))가 아닌 나머지 문자에 일치하는 경계(boundary)</td>
<td style="width: 11.0465%; height: 40px; text-align: justify;">r"\bain"<br>r"ain\b"</td>
</tr>
<tr style="height: 54px;">
<td style="width: 7.51163%; height: 54px; text-align: justify;">\B</td>
<td style="width: 63.6046%; height: 54px; text-align: justify;"><span style="background-color: #f9f9f9;">63개 문자에 일치하는 경계</span></td>
<td style="width: 11.0465%; height: 54px; text-align: justify;">r"\Bain"<br>r"ain\B"</td>
</tr>
<tr style="height: 20px;">
<td style="width: 7.51163%; height: 20px; text-align: justify;"><b>\d</b></td>
<td style="width: 63.6046%; height: 20px; text-align: justify;"><b>숫자 (0부터 9까지의 숫자)</b></td>
<td style="width: 11.0465%; height: 20px; text-align: justify;"><b>"\d"</b></td>
</tr>
<tr style="height: 20px;">
<td style="width: 7.51163%; height: 20px; text-align: justify;"><b>\D</b></td>
<td style="width: 63.6046%; height: 20px; text-align: justify;"><b>숫자가 아닌 것</b></td>
<td style="width: 11.0465%; height: 20px; text-align: justify;"><b>"\D"</b></td>
</tr>
<tr style="height: 20px;">
<td style="width: 7.51163%; height: 20px; text-align: justify;"><b>\s</b></td>
<td style="width: 63.6046%; height: 20px; text-align: justify;"><b>space 공백</b></td>
<td style="width: 11.0465%; height: 20px; text-align: justify;"><b>"\s"</b></td>
</tr>
<tr style="height: 36px;">
<td style="width: 7.51163%; height: 36px; text-align: justify;">\t</td>
<td style="width: 63.6046%; height: 36px; text-align: justify;">탭 (U+0009) 문자에 일치</td>
<td style="width: 11.0465%; height: 36px; text-align: justify;">\t</td>
</tr>
<tr style="height: 20px;">
<td style="width: 7.51163%; height: 20px; text-align: justify;"><b>\S</b></td>
<td style="width: 63.6046%; height: 20px; text-align: justify;"><b><span style="background-color: #f9f9f9;">space 공백이 아닌 것</span></b></td>
<td style="width: 11.0465%; height: 20px; text-align: justify;"><b>"\S"</b></td>
</tr>
<tr style="height: 20px;">
<td style="width: 7.51163%; height: 20px; text-align: justify;"><b>\w</b></td>
<td style="width: 63.6046%; height: 20px; text-align: justify;"><b>밑줄 문자를 포함한 영숫자 문자에 대응[A-Za-z0-9_] 와 동일</b></td>
<td style="width: 11.0465%; height: 20px; text-align: justify;"><b>"\w"</b></td>
</tr>
<tr style="height: 20px;">
<td style="width: 7.51163%; height: 20px; text-align: justify;"><b>\W</b></td>
<td style="width: 63.6046%; height: 20px; text-align: justify;"><b>\w 가 아닌 것</b></td>
<td style="width: 11.0465%; height: 20px; text-align: justify;"><b>"\W"</b></td>
</tr>
</tbody>
</table>
