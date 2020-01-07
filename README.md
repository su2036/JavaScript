# JavaScript - study
## ES6 === ES2015 시작하기!
### - 장점
- 가장 개선된 JavaScript문법입니다.
- ES6 Browser Compatibility, 호환성이 좋습니다.
- ES6 기반으로 한 JavaScript 생태계의 확산되고 있습니다.
  
<hr />  

# 1. SCOPE
## LET
### - ES6전
```
var name = "global var";        //var로 name 변수를 선언, 전역변수 값은 "global var"

function home () {
    var homevar = "homevar";    //var로 homevar 변수를 선언, 지역변수 값은 "homevar"
    for(var i=0; i<100; i++){
    }
    console.log(i);
}
home(); //1:20 scope chain?? 모르겠음.. 확인필요
```
- 결과  
![스크린샷 2020-01-07 오후 9 51 36](https://user-images.githubusercontent.com/29330085/71896756-f2b51d80-3197-11ea-973e-4e7282251845.png)  
>지역변수 값`(homevar)`을 먼저 찾고 그게 없다면, 전역변수로 `Scope Chain`을 따라 전역변수 값`(name)`을 찾습니다.

### - ES6
```
var name = "global var";        //var로 name 변수를 선언, 전역변수 값은 "global var"

function home () {
    var homevar = "homevar";    //var로 homevar 변수를 선언, 지역변수 값은 "homevar"
    for(let i=0; i<100; i++){
    }
    console.log(i);
}
home();
```
- 결과  
![스크린샷 2020-01-07 오후 9 54 08](https://user-images.githubusercontent.com/29330085/71896883-3f98f400-3198-11ea-89a5-1a078e8f5aec.png)  
>오류가 납니다.   
'i'라는 값은 `Block Scoup`, for문 안에서만 유효한 값입니다.

```
var name = "global var";        //var로 name 변수를 선언, 전역변수 값은 "global var"

function home () {
    var homevar = "homevar";    //var로 homevar 변수를 선언, 지역변수 값은 "homevar"
    for(let i=0; i<100; i++){
      console.log(i);
    }
}

home();
```
- 결과  
![스크린샷 2020-01-07 오후 9 52 39](https://user-images.githubusercontent.com/29330085/71896800-0b253800-3198-11ea-8894-8d034fafb062.png)  
>`for문 안`에서는 정상적으로 0~99까지 'i'값이 나옵니다.

마찬가지로 for문이 아닌 if문도
```
var name = "global var";        //var로 name 변수를 선언, 전역변수 값은 "global var"

function home () {
    var homevar = "homevar";    //var로 homevar 변수를 선언, 지역변수 값은 "homevar"
    for(let i=0; i<100; i++){
      //console.log(i);
    }
  if(true) {
    let testif = "test";        //let으로 testif 변수를 선언, 지역변수 값은 "test"
    console.log(testif)
  }
}

home();
```
- 결과  
![스크린샷 2020-01-07 오후 10 11 29](https://user-images.githubusercontent.com/29330085/71897852-162d9780-319b-11ea-9dc2-a7011f1d4f8b.png)  
>`if문 안(if문 안에서의 Block)`에서는 정상적으로 'test'가 나옵니다.

또, `if문 밖`에서는
```
var name = "global var";

function home () {
    var homevar = "homevar";
    for(let i=0; i<100; i++){
      //console.log(i);
    }
  if(true) {
    let testif = "test";
    //console.log(testif)
  }
  console.log(testif)
}

home();
```
- 결과  
![스크린샷 2020-01-07 오후 10 18 17](https://user-images.githubusercontent.com/29330085/71898053-a966cd00-319b-11ea-90c0-44d425291ada.png)
>에러가 나게 됩니다.

<hr />  

## LET과 CLOSURE
>closure상황을 만들어 "몇번째 리스트입니다."라는 출력을 하겠습니다.
- HTML
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
</head>
<body>
  <ul>
    <li>javascript</li>
    <li>java</li>
    <li>python</li>
    <li>django</li>
  </ul>
</body>
</html>
```
- Output
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>JS Bin</title>
    </head>
    <body>
    <ul>
        <li>javascript</li>
        <li>java</li>
        <li>python</li>
        <li>django</li>
    </ul>
    </body>
    </html>
  
- JavaScript
```
var list = document.querySelectorAll("li");
for(var i=0; i<list.length; i++) {
  list[i].addEventListener("click", function(){ 
    //list가 node list type인데 클릭을했을때?
    console.log(i + "번째 리스트 입니다.");
  }); 
}
```
- 결과
![스크린샷 2020-01-07 오후 10 49 24(3)](https://user-images.githubusercontent.com/29330085/71899936-21cf8d00-31a0-11ea-82e3-3e33e0bae314.png)  
>Output에 첫번째인 javascript, 두번째인 java 어떤 것을 누르더라도 콘솔에는 "4번쨰 리스트 입니다."라고 뜹니다.  
`closure`때문에 생기는 상황입니다.
```
list[i].addEventListener("click", function(){ 
    console.log(i + "번째 리스트 입니다.");
  }); 
```
>여기서 `function(){ 
    console.log(i + "번째 리스트 입니다.");
  }`이 콜백은   
  'i'는


