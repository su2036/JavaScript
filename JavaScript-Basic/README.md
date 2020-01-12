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


