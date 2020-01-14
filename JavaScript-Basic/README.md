# JAVASCRIPT - Basic Study


- 웹브라우저

```html
<html>
    <body>
        <input type =" button" onclick = "alert=('hello world')" value="hello world!" />
    </body>
</html>
```
> `"alert=('hello world')"` 이 부분이 자바스크립트로 경고창으로 `hello world!`가 뜨게 됩니다.

- 탈 웹브라우저  
: 웹서버를 동작하기 위한 도구로 사용(서버사이드 스크립트, Server-Side-Script)  
  - ex) node.js  
  ```javascript
  var http = require('http');
  http.createServer(function (req, res) {
      res.writeHead(200, {'Content-Type'; 'text/plain'});
      res.write('Hello World\n');
      res.end();
  }).listen(1337, '127.0.0.1');
  console.log('Server running at http://127.0.0.1:1337/');
  ```
> 127.0.0.1:1337에 접속시 `write`를 이용해 작성한 Hello World를 확인 할수 있습니다.  
node.js가 웹서버(apache2, nginx)와 같은 역활을 하게 됩니다.

- 탈웹
  - ex) Google Apps Script(구글 스프레드 시트) 도구 -> 스크립트 편집기  
```javascript
function onOpen(){
    var name = Browser.msgBox('Hello world');
}
```  
- 실습 결과  

![Uploading 스크린샷 2020-01-12 오후 4.01.38.png…](https://user-images.githubusercontent.com/29330085/72215346-4edfbf00-3555-11ea-89d7-99ec6e8abd2e.png)

![Uploading 스크린샷 2020-01-12 오후 4.01.38.png…](https://user-images.githubusercontent.com/29330085/72215355-6dde5100-3555-11ea-992f-557e03087a07.png)  
> `msgBox`를 이용해 alert와 같은 창이 뜨면서 'Hello world'가 뜨는 것을 확인 할 수 있다.

- 결론
  - 웹 브라우저 : alert
  - Node.js : write
  - SpreadSheet : msgBox  
  
  각각 환경에 따라 다른 명령을 사용해야 한다.

<hr />

## 주석  
- 한줄 주석 : //한줄 주석입니다.
```javascript
<script>//한줄 주석입니다.</script>
```

- 다중 주석 : /*  */
```javascript
<script>
    /*
    다중 주석입니다.
    다중 주석입니다.
    다중 주석입니다.
    */
</script>
```

<hr />

## 줄바꿈과 여백

### `;`(세미콜론) : 명령이 끝났다고 명시적으로 표현 하기 위함입니다.
+ cf) javascript에서 `;`을 안찍어도 실행은 됩니다. 자바스크립트는 `줄이 바뀌면 자바스크립트는 명령이 끝났다`고 간주하기 때문입니다. 그러므로 한줄로 쓸때는 `;`을 꼭 써줘야 합니다.

### 여백 : `TAB(탭)`을 이용해 `들여쓰기`가 가능하며 `띄워쓰기`를 이용하여 `가독성을 증가` 시킵니다.

<hr />

## 수의 표현
- JavaScript에서는 `"(큰따옴표)`나 '`(작은따옴표)`가 붙지 않은 숫자는 숫자로 인식합니다.  
  - ex)  
  ```javascript
  alert(1+1); //결과 2  
  alert(1.2 + 1.3); //결과 2.5
  ```
  ![](https://user-images.githubusercontent.com/29330085/72215970-f365ff00-355d-11ea-80df-157f1ffdb1e8.png)  
  

<hr />


## 수의 연산
### Math.pow => 제곱
- ex)   
```javascript
Math.pow(3,2);    //9,    3의 2승 
```
### Math.round => 반올림  
- ex) 
```javascript
Math.round(11.6); //12,   11.6을 반올림
```  
### Math.ceil => 올림  
- ex) 
```javascript
Math.ceil(3.1);   //4,    3.1을 올림
```  
### Math.floor => 내림  
- ex) 
```javascript
Math.floor(9.6);  //9,    9.6을 내림
```
### Math.sqrt => 제곱근  
- ex) 
```javascript
Math.sqrt(9);     //3,    3의 제곱근
```
### Math.random => 랜덤
- ex) 
```javascript
Math.random();    //0부터 1.0사이의 랜덤한 숫자
```

- ex) 응용
```javascript
Math.round(100 * Math.random());    //0~100사이 랜덤한 수
```
> `100 * Math.random()`에서 나온 소수점을 `Math.round`반올림을 이용해 정수가 나오게 됩니다. 

<hr />


## 문자
문자를 작성할 때는 `""(큰따옴표)`를 이용한 사이에 작성해야 합니다.  
cf) `"(큰따옴표)로 시작해 끝도"(큰따옴표)`, 또는 `'(작은따옴표)로 시작해서 끝도'(작은따옴표)`로 시작과 끝이 같아야 합니다.
- ex) '(작은따옴표)로 시작해서 '(작은따옴표)로 끝나는 사이에 '(작은따옴표)를 넣고 싶을때 `\(역슬래쉬)`를 넣는다.

```javascript
alert('I\'m Student');  //\(역슬래시)를 이용해 '을 문자로 escape합니다.
```
![\이용](https://user-images.githubusercontent.com/29330085/72216250-24483300-3562-11ea-8dbd-34d0aeb5bd4e.png)

## 문자열(String)
`typeof` : 문자인지 숫자인지 확인할때 사용하면 됩니다.

- ex) 숫자
```javascript
typeof 1
```
- ex) 문자
```javascript
typeof "1"
```  
![숫자문자](https://user-images.githubusercontent.com/29330085/72216307-c700b180-3562-11ea-8eb3-8442398181a7.png)
- ex) 문자열
```javascript
typeof "abcde"
```  
![문자열](https://user-images.githubusercontent.com/29330085/72216306-c700b180-3562-11ea-8131-cb80381c0c79.png)  


<hr />

## 문자의 연산
`\n`을 이용하면 줄바꿈이 일어납니다.

- 문자와 문자를 더할때
```javascript
alert("abc" + "def"); // abcdef
```
- 문자의 길이를 구할때는 .length
```javascript
alert("abc def");   //7, 공백을 포함합니다.
```
- cf) 1 + 1과 "1" + "1"
```javascript
alert(1 + 1);   //2, 숫자를 더합니다.
```
```javascript
alert("1" + "1");   //11, 숫자인 문자와 숫자인 문자를 더합니다.
```
- 결과  
![문자+문자결과](https://user-images.githubusercontent.com/29330085/72216512-442d2600-3565-11ea-9fd7-6cf04ec7dffa.png)

- Cf) 원시타입(primitive type)과 참조타입(reference type)
link : https://ryulog.tistory.com/140

<hr />

# 변수
## 변수의 사용법
> 변수(Variable)는 (문자나 숫자 같은) 값을 담는 그릇,컨테이너로 `값을 유지할 필요`가 있을 때 사용합니다.   
또 여기에 담겨진 값은 `다른 값으로 바꿀 수 있습니다.`  
JavaScript에서 변수는 `var`로 시작합니다.
- 예제
```javascript
var a = 1;      // var는 생략이 가능 하나 왜 생략을 하는지 알고 생략을 해야함.
alert (a+1);    // 2
```
- 결과  
![스크린샷 2020-01-13 오후 8 41 26](https://user-images.githubusercontent.com/29330085/72253578-33ec7800-3645-11ea-9f56-654075ca57be.png)
![스크린샷 2020-01-13 오후 9 02 18](https://user-images.githubusercontent.com/29330085/72254627-0228e080-3648-11ea-9371-6685b2f173e2.png)
> a = 2 에서 3으로 바꾸고 2일때 a + b를 했던 것 그대로 하면 a(3)+b(1)으로 4라는 결과를 볼 수 있습니다.

- 예제, 변수에 숫자가 아닌 문자열도 가능합니다.
```javascript
var first = 'coding';
console.log(first + ' everybody');
```
- 결과  
![스크린샷 2020-01-13 오후 9 13 52](https://user-images.githubusercontent.com/29330085/72255260-9d6e8580-3649-11ea-9856-271dae12773a.png)  
> 처음 변수를 사용할 때에는 `var` 붙여서 선언해 준 뒤 그다음 부터는 `var 없이` 사용할 수 있습니다.  
- 결과   
![스크린샷 2020-01-13 오후 9 16 39](https://user-images.githubusercontent.com/29330085/72255415-00f8b300-364a-11ea-82e9-f061a7f2138e.png)

> 또 다른 방법은 `var를 한번 사용한 뒤` 변수를 한 줄로 붙여서 사용도 가능합니다.
```javascript
var a = 'coding', b = ' everybody';
console.log(a + b);
```
- 결과  
![스크린샷 2020-01-13 오후 9 19 12](https://user-images.githubusercontent.com/29330085/72255553-5cc33c00-364a-11ea-9825-be10ffae786b.png)  

## 변수의 효용
> 변수는 코드의 재활용성을 높여 주기 때문에 사용합니다.
- 예제, 변수가 없다면 100에 10을 더하고, 10을 나눈 후, 다시 10을 뺴고 거기에 10을 곱해야 할때.
```javascript
console.log(100+10);
console.log((100+10)/10);
console.log(((100+10)/10)-10);
console.log((((100+10)/10)-10)*10);
```
- 결과  
![스크린샷 2020-01-13 오후 9 30 59](https://user-images.githubusercontent.com/29330085/72256225-01924900-364c-11ea-9052-52dc3d92dc64.png)  
> 이런식으로 일일이 다 타이핑 해야되는 상황이 생기게 됩니다.

- 예제, 위 상황에서 변수를 사용할 경우
```javascript
var a = 100;        // 여기에 a는 변할수 있는 영역
a = a + 10;         // 여기서 부터는 변하지 않는 영역
console.log(a);
a = a / 10;
console.log(a);
a = a -10;
console.log(a);
a = a * 10;
console.log(a);
```
> 변수를 사용한 위 코드에서는 첫번째 줄의 100을 다른 숫자로 바꾸면 나머지 아래 로직에 대입되는 변수의 값이 모두 바뀌게 됩니다.   
그러면서 아래 나머지 로직에서는 수정할 필요가 없는 `변하지 않는 영역`이라고 할 수 있습니다.

<hr />

# 비교
## 연산자
> 연산자는 `어떠한 작업을 컴퓨터에 지시하기 위한 기호`라고 할 수 있습니다.

```
a = 1
```
> 'a'는 변수, '1'은 값(상수)이며 좌항의 변수 'a'에 우항의 값인 '1'을 대입한다 라는 '='은 `대입연산자(이항연산자)`라고 합니다.
- cf) 상수 : 변하지 않는 값, 변수 : 변하는 값

## 비교 연산자 : ==(동등연산자), ===(일치연산자)
> 좌항과 우항이 같은지 비교하는 연산자인 `비교연산자`입니다.  
비교연산자를 통해 `True`와 `False`라는 값을 받습니다. 이러한 것을 `블린(booolean)`이라고 불립니다.

### == : 동등연산자(equal operator)
> 좌항과 우항을 비교해서 서로 값이 같다면 `True`, 다르다면 `False`가 됩니다.
- 예제
```javascript
console.log(1==2);
console.log(1==1);
console.log("one" == "one");
console.log("one" == "two");
```
- 결과  
![스크린샷 2020-01-13 오후 10 00 44](https://user-images.githubusercontent.com/29330085/72257948-34d6d700-3650-11ea-8c3d-8f31f03203a6.png)
> 이걸 하는 이유는 조건문에서 확인하기 위해 사용합니다.

### === : 일치연산자(strict operator)
> 좌항과 우항이 `'정확'`하게 같을 때 `True`, 다르면`False`가 됩니다.
- 예제
```javascript
console.log(1 === '1'); // false    int형 1과 string 1이라는 데이터 타입이 다르기 떄문에 false가 됩니다.
console.log(1 == '1');  // true     int형 1과 string 1이라는 데이터 타입이더라도 1로 같기 때문에 true가 됩니다.
```
- 결과  
![스크린샷 2020-01-13 오후 10 07 47](https://user-images.githubusercontent.com/29330085/72258343-263cef80-3651-11ea-9392-08333362c0e5.png)

> 좌항과 우항의 `정보가 같을 뿐만 아니라 데이터의 형식`이 정확하게 같아야 True가 됩니다.  
동등연산자는 `데이터타입이 다르더라도 실질적으로 갖고있는 정보`가 같다면 True가 됩니다.  
프로그래밍에서는 `정확`한 값이 비슷한 값보다 세세한 버그를 일으키지 않는 방법입니다.  
그러므로 `꼭! ===를 사용`하도록 해야합니다.


<hr />







# 함수
> 함수(function)란 하나의 로직을 재실행 할 수 있도록 하는 것으로 코드의 재사용성을 높여줍니다.
- 문법
```javascript
function 함수명( [인자...[,인자]] ){
코드
return 반환값
}
```
## 함수호출
- 예제
```javascript
function numbering(){
document.write(1);
}
numbering();
```
- 결과  
![스크린샷 2020-01-14 오전 1 45 26](https://user-images.githubusercontent.com/29330085/72274449-8d699c80-366f-11ea-9b7e-03968c4e2be6.png)


