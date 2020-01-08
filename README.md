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
'i'라는 값은 `Block Scope`, for문 안에서만 유효한 값입니다.

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
Block Scope가 존재합니다. 'i'를 지역변수화 시킨 개념과 비슷합니다.  
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

##### TIP)
1. `const를 기본으로` 사용합니다.
1. 만약 변경이 될 수 있는 변수는 `let`을 사용합니다.
1. ES2015에서는 `var는 사용하지 않는다.`  

<hr />  

## CONST 특성과 IMMUTABLE ARRAY

```
function home() {
    const list = ["apple", "orange", "watermelon"];
    list.push("banana");
    console.log(list);
}
home();
```  
- 결과  
![스크린샷 2020-01-08 오전 1 58 56](https://user-images.githubusercontent.com/29330085/71913310-77b12e80-31ba-11ea-8c46-2eb1b200bf0f.png)

##### TIP)
1. const를 사용하더라도 `배열과 오브젝트의 값을 변경하는 것은 가능`합니다.
1. 값을 `재할당 하는 것만 불가능`합니다.

### immutable array
> "immutable array를 어떻게 만들까?" => 뒤로가기, 앞으로가기 등 데이터를 되돌리고 싶은 경우(copy가 되는게 아니라 계속 바뀌기 떄문에 기억을 할 수 없습니다.)

```
function home() {
    const list = ["apple", "orange", "watermelon"];
    list.push("banana");            //list배열 끝에 "banana"를 '뒤'에 추가합니다.
    console.log(list);
}
const list = ["apple", "orange", "watermelon"];
list2 = [].concat(list, "banana");  //list(["apple", "orange", "watermelon"])값에 "banana"를 합친 값을 list2에 할당합니다.
console.log(list, list2);
```  
- 결과  
![스크린샷 2020-01-08 오전 2 41 50](https://user-images.githubusercontent.com/29330085/71916068-72ef7900-31c0-11ea-87c6-08da1e8ac134.png)  

##### TIP)
1. const 값을 재할당 하는 것은 불가능하지만 `할당된 객체의 내용(프로퍼티의 추가, 삭제, 프로퍼티 값의 변경)은 할 수 있다.`  
    - ex)
    ```
    const user = { name : 'Bae' };  //JSON 변수 user에 name을 키로 하고 
                                      'Bae'를 값으로 하는 json 객체를 할당합니다.
    user.name = 'Geum';             //이후 JSON 변수 user의 name 키의 값을 
    console.log(user);                'Geum'으로 변경합니다.
    ```  
    ##### 참조 : https://poiemaweb.com/es6-block-scope  

<hr />  

## ES2015 String에 새로운 메서드들
```
let str = "hello world ! ^^ ~~"; 
let matchstr = "hello"; //"hello"의 길이랑 위 str = "hello"의 길이랑 비교합니다.
```  
```
console.log(str.startsWith(matchstr));
```  
>시작 때 문자열이 일치하는지 확인 가능합니다.(공백 포함)
- 결과  
![스크린샷 2020-01-08 오전 3 18 50](https://user-images.githubusercontent.com/29330085/71918468-aa145900-31c5-11ea-80e5-26cbb4c42c8b.png)

```
console.log(str.endsWith(matchstr)); 
```  

>끝으로 끝나는 복수 문자열이 일치하는지 확인 가능합니다.(공백 포함)
- 결과  
![스크린샷 2020-01-08 오전 3 21 44](https://user-images.githubusercontent.com/29330085/71918618-02e3f180-31c6-11ea-9fe3-d9332dd45d54.png) ![스크린샷 2020-01-08 오전 3 21 03](https://user-images.githubusercontent.com/29330085/71918574-ecd63100-31c5-11ea-8297-6b95016ccaf4.png) 


```
console.log(str.includes("^"));
```
>매칭되는 문자열이 있는지 확인 가능합니다.
- 결과  
![스크린샷 2020-01-08 오전 3 23 11](https://user-images.githubusercontent.com/29330085/71918723-39217100-31c6-11ea-9231-2fbb9a69e0dd.png)  

<hr />

# 3. ARRAY
## FOR OF - 순회하기  
Array의 순회를 알아보겠습니다. Array의 `for of`가 ES6에서 생겼습니다.
### FOR문  
- 예시
```
var data = [1, 2, undefined, NaN, null, ""];
for(var) i=0; i<data.length; i++){
  console(i);
}
```  
- 결과  
![스크린샷 2020-01-08 오후 11 25 18](https://user-images.githubusercontent.com/29330085/71985860-be606080-326e-11ea-9005-cdfb965131a8.png)  

### FOREACH
>forEach는 for문과 마찬가지로 반복적인 기능을 수행할 때 사용합니다.
하지만 for문처럼 index와 조건식, increase를 정의하지 않아도 callback 함수를 통해 기능을 수행할 수 있습니다.
```
var data = [1, 2, undefined, NaN, null, ""];
data.forEach(function(value){
  console.log("valueis", value);
});
```
- 결과  
![스크린샷 2020-01-08 오후 11 44 38](https://user-images.githubusercontent.com/29330085/71987099-e4870000-3270-11ea-8d20-7b1a15e15f1f.png)  

### FOR IN

```
var data = [1, 2, undefined, NaN, null, ""];

Array.prototype.getIndex = function(){};

for(let idx in data) {
  console.log(data[idx]);
}
```
- 결과  
![스크린샷 2020-01-08 오후 11 53 55](https://user-images.githubusercontent.com/29330085/71987785-2b292a00-3272-11ea-8e19-078d5cff0e7c.png)  
>자신이 갖고 있지 객체 이외에 프로토타입 객체를 이용해 'getIndex'와 같은 객체도 포함될 수 있다는 문제가 있습니다. 

### FOR OF
```
var data = [1, 2, undefined, NaN, null, ""];

Array.prototype.getIndex = function(){};

for(let value of data) {
  console.log(value);
}
```
- 결과  
![스크린샷 2020-01-09 오전 12 05 25](https://user-images.githubusercontent.com/29330085/71988721-c1aa1b00-3273-11ea-953d-bb889b18b0a2.png)
>`Array.prototype.getIndex = function(){};`값이 나오지 않았습니다. 
순회할때는 `index가 아닌 value로 순회가 가능`하므로 `for in`의 문제를 방지할 수 있습니다. 

  - Cf) 
  ```
  var str = "hello world!!!!";
  for(let value of str){
    console.log(value);
  }
  ```  
  - 결과  
  ![스크린샷 2020-01-09 오전 12 24 04](https://user-images.githubusercontent.com/29330085/71990296-76453c00-3276-11ea-878d-8341e38bed24.png)  
  >문자열을 character(문자)단위로 순회하며 출력 해줍니다.
- TIP)
  - 절대 배열에서 `for-in`을 쓰면 안됩니다.

## SPREAD OPERATOR - 배열의 복사  
> spread operator, 펼침연산자 = [`...`arr]로 표기합니다.

```
let pre = ["apple", "oragne", 100];
let newData = [...pre];     //[...pre] = ["apple", "oragne", 100]
console.log(pre,newData);
```  
- 결과  
![스크린샷 2020-01-09 오전 12 40 09](https://user-images.githubusercontent.com/29330085/71992392-a8579d80-3278-11ea-9054-c1d641acf770.png)
> 기존에 참조를 끊고 `메모리에 새로운 공간에 새로운 배열로 들어간 것` 입니다.  'pre'와 'newData'는 서로 같은 참조를 유지 하지 않습니다. 완전히 `복사`를 한 것 입니다.  
`Array.prototype.concat`을 이용해 합칠 경우, 새로운 배열을 복사해 반환하는 것과 같은 것입니다.


## SPREAD OPERATOR - 몇가지 활용  
### ex1)
```
let pre = [100,200, "hello", null];

let newData = [0, 1, 2, 3, ...pre, 4];

console.log(newData);
console.log(pre === newData);
```  
- 결과  
![스크린샷 2020-01-09 오전 12 40 09](https://user-images.githubusercontent.com/29330085/71999748-52d5bd80-3285-11ea-98a0-3136713ec0c4.png)  
> 배열을 어떤 특정 배열에 열거할 수 있습니다.
### ex2)

```
function sum(a,b,c) {
  return a+b+c;
  
}
let pre = [100,200,300];

console.log(sum.apply(null, pre));//apply()는 배열로된 하나의 인자를 받습니다.
                                    null인자의 역할은 호출하는 this를 대체하는 것입니다.
console.log("result=>", sum(...pre));
```
![스크린샷 2020-01-09 오전 2 09 50](https://user-images.githubusercontent.com/29330085/71999643-23bf4c00-3285-11ea-821f-4e815489f9fa.png)  
> (sum.apply(null, pre))에서 apply는 하나의 인자로 묶어 배열로 만들어 넣는 것입니다.  
sum(...pre)은 즉, sum(100,200,300)으로 될것이며, 배열값을 각각에 다양한 메개변수 할당이 쉬워졌습니다.  
   
  - 결국 배열을 바꾸지 않고 새로운 값을 복사합니다.  
  배열을 합치거나 펼쳐진상태로 배열을 새로운 파라미터 형태로 전달 해줄때 `spread operator`가 유용합니다.

## FROM 메서드로 진짜 배열 만들기
 
//객체 arguments => 가변적인 파라미터일 경우에 가끔 씁니다.

### MAP
> 순회를 하면서 필요한 값을 추가하고 새로운 값을 반환합니다.
```
function addMark() {
  let newData = arguments.map(function(value){ //가짜배열
    return value + "!";
  });
  console.log(newData);
}
addMark(1,2,3,4,5,6,7,8,9);
```  
- 결과  

> 



- 해결방법 
### FROM
> 순회를 하면서 필요한 값을 추가하고 새로운 값을 반환합니다.
```
function addMark() {
  let newArray = Array.from(arguments);   //arguments로 부터 배열을 만든다.
  let newData = newArray.map(function(value){
    return value + "!";
  });
  console.log(newData);
}
addMark(1,2,3,4,5,6,7,8,9);
```  
- 결과  
  ![스크린샷 2020-01-09 오전 3 00 32](https://user-images.githubusercontent.com/29330085/72003216-36894f00-328c-11ea-9702-43230e47ddfc.png)
>`from`함수를 사용하면 유사 배열을 배열로 만들어준다.
가령, DOM조작시 querySelectAll로 얻은 노드 리스트를 from 을 통해 배열로 변경할 수도 있다.
가짜 배열을 진짜 배열로 만든다.

<hr />

## 실습 예제
```
function print() {
  /*
  filter, inlues, from을 사용해서 문자열'e'가 포함된 노드로 구성된 배열을 만들어서 반환합니다.
}
print();
```
- 확인필요