# FUNCTION(함수)
## Arrow Function
- `setTimeout`사용법
> `setTimeout`('함수',시간);
```javascript
setTimeout(function(){          // 콜백함수
    console.log("settimeout");
}, 1000);                       // 1초
```
> setTimeout(function() => 축약해서 사용하기
```javascript
setTimeout( ()=>{
    console.log("settimeout arrow");
}, 1000);
```

     
> 동일하게 1초 뒤에 "settimeout arrow"가 출력되는 것을 확인 할 수 있습니다.

- 반환값이 경우 효율적으로 사용
```javascript
let newArr = [1, 2, 3, 4, 5].map(function(value, index, object) {   //value인자는 현재 배열 요소(1,2,3,4,5)알겠는데 index는 0부터시작(초기화), object(현재돌고있는 배열 자체)는 왜 들어가지?? => 맞는지 확인!
    return value * 2;
});

console.log(newArr);
```
- 결과
> 2,4,6,8,10

- 궁금증의 코드 확인필요!
```javascript
let testarr = [1, 2, 3, 4, 5];  // 원본배열

let newArr = testarr.map(function(value, index, array) {
    return value * 2;       // 배열의 모든 요소에 2를 곱함, 매서드 수행 후 리턴값은 새로운 배열
});
console.log(testarr);       // 매서드 수행 후 원본 배열
// [1, 2, 3, 4, 5]
console.log(newArr);        // 매서드 수행 후 생성된 배열
// [2, 4, 6, 8, 10]
```
- 궁금증 코드 결과  
![스크린샷 2020-01-22 오전 8 02 21](https://user-images.githubusercontent.com/29330085/72850938-9dc3ec00-3ced-11ea-930a-d6701a493c8e.png)  

- 축약
```javascript
let newArr = [1, 2, 3, 4, 5].map((v) => {       // 콜백함수 인자가 긴것을 축약가능
    return v * 2;
});

console.log(newArr);
```
- return 생략
```javascript
let newArr = [1, 2, 3, 4, 5].map((v) => v * 2); // return을 생략하면서 v에 2를 곱해서 반환
console.log(newArr);
```
> `map((v) => v * 2)`을 이용해서 기존 `return v * 2`의 return을 생략해서 사용 가능하며,
`map((v) => (v * 2))`이런 방식으로도 생략을 해서 반환을 받을 수 있습니다.
- 결과
> 2,4,6,8,10  
![스크린샷 2020-01-22 오전 8 07 44](https://user-images.githubusercontent.com/29330085/72851181-4a05d280-3cee-11ea-9194-f777d89a1cb7.png)  


## Arrow function의 `this context`
> context 문제로 보통 bind를 쓴다.  
this context(실행 컨텍스트)는 컨텍트라고도 부르며 `전역 컨텍스트`와 `함수 컨텍스트` 두가지 타입이 존재합니다.  

  - 함수 컨텍스트
    > 함수를 호출하면서 독자적인 실행 컨텍스트가 생성됩니다. 실행 컨텍스트는 변수객체가 연결되어 있습니다.

  - 전역 컨텍스트
    > 가장 바깥쪽에 존재하는 실행 컨텍스트입니다. 이 또한 실행 컨텍스트이며 가장 상위에 있기 때문에 전역 컨텍스트라고 부릅니다.  
    웹 브라우저에서는 이 컨텍스트를 window라고 부르며 실행컨텍스트에 경우 보통 포함된 코드가 모두 실행될 때 파괴되는데, `전역컨텍스트`는 어플리케이션이 종료될 때, 예를들어 웹페이지에서 나가거나 브라우저를 닫을 때까지 계속 유지 됩니다.

```javascript
const myObj = {
    runTimeout() {
        setTimeout(function() {
            console.log(this === window);   // this가 가르키는게 window인가?
        }, 200);    // 2초뒤 출력
    }
};
myObj.runTimeout();
```
- 결과
TRUE로 this가 가르키는 것은 window라는 것을 확인 가능합니다.  

- `This`란?
> this 는 현재 `실행문맥`입니다. 즉, `실행문맥`이란 호출자가 누구냐는 것과 같습니다.
```javascript
alert(this === window); // true, 호출자는 window
```

- 예제2
    ```javascript
    const myObj = {
        runTimeout() {
            setTimeout(function() {
                this.printData();   // this가 myObj가 아닌 PrintData()를 호출,
            }.bind(this), 200);     // 함수를 bind로 감싸주면서 오브젝트 안에 오브젝트를 호출
        },
        printData() {
            console.log("hi codesquad!");
        }
    };
    myObj.runTimeout();
    ```
    - 결과  
    ![스크린샷 2020-01-22 오전 8 33 43](https://user-images.githubusercontent.com/29330085/72852463-eaa9c180-3cf1-11ea-9985-1f374610f7aa.png)  

## Default Parameters (기본 메개변수)

```javascript
function sum(value, size) {     // size가 defalut paramater
    size = size || 1;           // 두번째 인자 즉, size에 아무것도 없으면 size는 1로 됨
    return value * size;
}
console.log(sum(3, 10));        // 30, value(3) * size(10) 
```
- 예제, 오브젝트다!
```javascript
function sum(value, size = {value:1}) {     // size에 아무것도 없으면 size 오브젝트는 1로 됨
    return value * size.value;
}
console.log(sum(3, {value:3}));        // 9, value(3) * size (object:3) 
```

## Rest Parameters
- `Rest parameter`는 정해지지 않은 수(an indefinite number, 부정수)인수를 배열로 나타낼 수 있게 합니다.

- 기본문법
```javascript
function foo(...rest) {
    console.log(Array.isArray(rest));   // true
    console.log(rest);                  // [1, 2, 3, 4, 5], 배열로 출력
}
foo(1,2,3,4,5);
```
- 기본문법 결과  
![스크린샷 2020-01-22 오전 9 13 23](https://user-images.githubusercontent.com/29330085/72854357-7540ef80-3cf7-11ea-8274-cd4c0e7bf219.png)

> Rest파라미터(Rest Parameter, 나머지 매개변수)는 매개변수 이름 앞에 3개점 `...`을 붙여서 정의한 매개변수를 의미합니다. Rest파라미터는 함수에 전달된 인수들의 목록을 배열로 전달받습니다.  
함수에 전달된 인수들은 순차적으로 `파라미터`와 `Rest파라미터`에 할당 됩니다.

- 예시, 
```javascript
function bar(param1, param2, ...rest) {
    console.log(param1);     // 1
    console.log(param2);     // 2
    console.log(rest);       // [3, 4, 5]
}
bar(1,2,3,4,5);
```
- 결과  
![스크린샷 2020-01-22 오전 9 19 32](https://user-images.githubusercontent.com/29330085/72854658-542cce80-3cf8-11ea-8634-577768fb6590.png)

> rest 파라미터는 이름 그대로 먼저 선언된 파라미터에 할당된 인수를 제외한 나머지 인수들이 모두 배열에 담겨 할당됩니다. 따라서 Rest파라미터는 반드시 마지막 파라미터이어야 합니다.

<hr />
- es3..?
```javascript
function checkNum() {
    const argArray = Array.prototype.slice.call(arguments);
    console.log(argArray);
    console.log(toString.call(arguments));
}
const result = checkNum(10,2,3,4,5,"66");
```

```javascript
function checkNum() {
    const argArray = Array.prototype.slice.call(arguments);
    console.log(argArray);
    console.log(toString.call(arguments));
    const argArray.every((v) => typeof v === "number")
    console.log(result);
}
const result = checkNum(10,2,3,4,5,"66");
```
