# 함수지향 - 유효범위
> 유료범위(Scope)는 변수의 수명을 의미합니다.

## 전역변수와 지역변수

- 예제
```js
let vscope = 'global';

function fscope(){
    alert(vscope);
}
fscope();       // 'global'
```
> fscope는 함수 안이 아닌 밖인 vscope에 접근할 수 있습니다.

- 예제
```js
let vscope = 'global';

function fscope(){
    let vscope = 'local';
    alert(vscope);
}
fscope();       // 'local'
```
> fscope함수 안에 vscope라는 변수가 선언되어있기 때문에 `alert(vscope)`는 가까운 vscope인 함수 안에 있는 `vscope = 'local';`을 향하며 결과는 `local`을 볼 수 있습니다.  
 여기서 함수 내에 있는 `vscope를 지역 변수`라고 하며 위 예제에서 보면 맨 첫라인에 `vscope를 전역변수`라고 합니다.

- 추가예제
```js
let vscope = 'global';

function fscope(){
    vscope = 'local';
}
fscope();       
console.log(vscope);    // 'local'
```
- 결과  
![스크린샷 2020-02-10 오전 12 26 25](https://user-images.githubusercontent.com/29330085/74104821-fe7f6f80-4b9b-11ea-9e66-bd107bb1c171.png)

    > 함수내에 `let을 생략한 vscope = 'local';`을 쓰게 되면 전역변수 vscope의 global값을 'local'을 할당하여 결과는 `local`이 나오게 됩니다.


## 유효범위의 효용성
- 예제
```js
function a (){
    let i = 0;
}
for(let i = 0; i < 5; i++){
    a();
    document.write(i);     // 0,1,2,3,4
}
```
- 예제
```js
function a (){
    i = 0;              // let을 생략한 i = 0;을 씀
}
for(let i = 0; i < 5; i++){
    a();
    console.log(i);     // 무한반복...
}
```
> `let i = 0;`이 아닌 `i = 0;`으로 하게되면 무한반복이 되는데 그 이유는 for문 안에 i 값이 전역변수가 되며 a함수를 호출하면서 i의 값이 `let`이 붙어있지 않음으로 인해 전역변수가 되어 `0으로 초기화`가 되는 a함수가 실행 되어 5보다 작기 때문에 무한 반복이 됩니다.  
이러한 문제를 해결하기 위해 전역변수, 지역변수를 사용하게 됩니다.


## 전역변수를 사용하는법
- 예제, 불가피하게 전역변수를 사용해야 하는 경우는 하나의 객체를 전역변수로 만들고 객체의 속성으로 변수를 관리하는 방법을 사용합니다.
```js
let MYAPP = {}      // 전역 변수
MYAPP.calculator = {    // calculator 속성, 속성(객체 안에 있는 변수)
    'left' : null,
    'right' : null
}
MYAPP.coordinate = {
    'left' : null,
    'right' : null
}
 
MYAPP.calculator.left = 10;
MYAPP.calculator.right = 20;
function sum(){
    return MYAPP.calculator.left + MYAPP.calculator.right;
}
document.write(sum());
```

- 예제, 전역변수를 사용하고 싶지 않다면 익명함수를 호출함으로서 이러한 목적을 달성할 수 있습니다.
```js
(function(){
    let MYAPP = {}          // 함수안에 선언된 변수, 지역변수
    MYAPP.calculator = {
        'left' : null,
        'right' : null
    }
    MYAPP.coordinate = {
        'left' : null,
        'right' : null
    }
    MYAPP.calculator.left = 10;
    MYAPP.calculator.right = 20;
    function sum(){
        return MYAPP.calculator.left + MYAPP.calculator.right;
    }
    document.write(sum());
}())
```
> 바로 호출 해서 쓸때는 ()를 이용하며, `()`는 익명함수 이다.

## 유효범위의 대상
> javascirpt는 함수에 대한 유효범위만 제공합니다. 많은 언어들이 블록(대체로 '{}')에 대해서

- 예제
```java
for(int i = 0; i < 10; i++){
    String name = "Changsu";    // String name = let name 
}
System.out.pritnln(name);       // System.out.println(name) = console.log(name)
```
> for문 안에 `String name = "Changsu";`라고 지역변수가 선언되어 있기 떄문에 자바는 자바스크립트와 다르게 `for문 블록('{}')안이 아닌 밖에서 호출`하면 `에러`가 납니다.

## 정적 유효범위
> 자바스크립트는 함수가 선언된 시점에서 유효범위를 갖습니다.   
유효 범위의 방식을 `정적 유효범위(static scoping) 또는 렉시컬(lexical scoping)`이라고 합니다.

- 에제
```js
let i = 5;      // 전역변수

function a(){
    let i = 10; // 지역변슈
    b();
}

function b(){   // 호출된 함수 a가 아닌 정의될때의 전역변수 i가 사용됩니다.
    document.write(i);
}

a();
```
- 결과  
![스크린샷 2020-02-10 오전 9 11 29](https://user-images.githubusercontent.com/29330085/74113095-5bebde80-4be5-11ea-833f-ed73ba9fe143.png)  

> `document.write(i)`여기 i는 함수 b가 호출한 a함수에 지역변수`i=10`이 아닌 정의된 전역변수`let i = 5`가 되어 결과는 5가 출력되는 것을 확인 할 수 있습니다. 이러한 것을 `정적 유효범위`, 또는 `렉시컬` 이라고 합니다. 


