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
'i'라는 값은 `Block Scop`, for문 안에서만 유효한 값입니다.

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
  }`이 콜백은 나중에 실행되는 것인데 그때마다 function이가지고있는 이 'i'는 `전역변수도 아니고 지역변수도 아닙니다.`  
  콜백 밖에 `for(var i=0; i<list.length; i++)`여기 'i'값을 참조 하는데 이 'i'값이 계속 변경이 되면서 4개 이벤트 콜백 함수, 이벤트 핸들러가 4개입니다. for문에서 밖에 있는 'i'값을 계속해서 참조하게 되면서 마지막 값인 4가 되어 모두 공유해 어떤걸 눌러도 "4번째 리스트 입니다."가 되는 것 입니다.

- 문제 해결 `var -> let`  

```
var list = document.querySelectorAll("li");     //
for(let i=0; i<list.length; i++) {              //
  list[i].addEventListener("click", function(){ //
    console.log(i + "번째 리스트 입니다.");
  }); 
}
```

- 결과  
![스크린샷 2020-01-07 오후 11 49 13](https://user-images.githubusercontent.com/29330085/71903861-5ba49180-31a8-11ea-9774-7220a350dd6f.png)  
>`var`를 `let`으로 바꿔 줌으로써 이렇게 순차적으로 나오는 것을 확인 할 수 있습니다.  
Block Scop가 존재합니다. 'i'를 지역변수화 시킨 개념과 비슷합니다.  
그러면서 'i'값이 0부터 시작하게 됩니다.

<hr />  

## CONST - 선언된 변수 지키기
```
function home() {               
  var homename = 'my house';    //var로 선언된 변수 homename은 my house가 할당됩니다.
  homename = "your house";      //homename은 다시 your house가 할당 됩니다.
  console.log(homename);
}

home();
```  
- 결과  
![스크린샷 2020-01-08 오전 1 13 22](https://user-images.githubusercontent.com/29330085/71910338-12a70a00-31b5-11ea-8101-c35132c1be9b.png)  
> 'your house'결과를 확인 할 수 있습니다.

### `var -> const`
```
function home() {
  const homename = 'my hous';
  homename = "your house";
  console.log(homename);
}

home();
```
- 결과  
![스크린샷 2020-01-08 오전 1 26 50](https://user-images.githubusercontent.com/29330085/71910829-fce61480-31b5-11ea-9b9b-081e6089b8f8.png)  
>constant배열에 할당하면 안된다고 합니다. `const가 상수로 할당` 하므로 'my house'에서 'your house'로 할당하지 않도록 합니다.  

- 문제 해결  
```
function home() {
  const homename = 'my hous';
  //homename = "your house";    //주석처리로 없앱니다.
  console.log(homename);
}

home();
```  
- 결과  
![스크린샷 2020-01-08 오전 1 36 06](https://user-images.githubusercontent.com/29330085/71911568-46832f00-31b7-11ea-9111-f0cc702c75ab.png)  
>그대로 `homename에 'my house'가 할당`되어 결과를 보여줍니다.  
cf) Type에 상관 없이 const 재할당 할 수 없습니다.  
- ex)   
```
function home() {
  const homename = [1,2,3,4]];
  homename = ["1","2"]];
  console.log(homename);
}

home();
```  
> 이 또한 재할당을 할 수 없으므로 에러가 나게 됩니다.

#### TIP)
1. `const를 기본으로` 사용합니다.
1. 만약 변경이 될 수 있는 변수는 `let`을 사용합니다.
1. `var는 사용하지 않는다.`