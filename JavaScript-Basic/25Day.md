# 객체지향 - 데이터 타입
## 원시 데이터 타입과 객체
> 데이터 타입이란 데이터의 형태를 의미합니다. 데이터 타입은 크게 두가지로 구분할 수 있습니다.  
객체와 객체가 아닌 원시데이터 타입(primitive type)이라고 합니다. 

- 원시 데이터 타입 종류
  - 숫자
  - 문자열
  - 불리언(true/false)
  - null
  - undefined


## 레퍼 객체
- 예제
```js
let str = 'coding';
console.log(str.length);    // 6, 문자열 길이
console.log(str.charAt(0)); // "c" 문자 글자
```
> str`.`이 `Object Access Operator`라는 객체 접근 연산자 입니다.  
`.`앞에 있는 str이 객체를 의미하게 됩니다.  
즉, 문자열(coding)이 객체라는 것 입니다. `원시 데이터 문자열이 객체이어야 작업`들을 할 수 있게 됩니다.

- 예제
```js
let str = 'coding';
str.prop = 'everybody';     // 객체가 만들어지고 끝남, 그리고 원래 원시데이터로 바뀜
console.log(str.prop);      // undefined
```
> str.prop를 하는 순간에 자바스크립트 내부적으로 String 객체가 만들어 집니다. prop프로퍼티는 이 객체에 저장되고 이 객체는 곧 끝나면서 제거 됩니다.   
그렇기 떄문에 prop라는 속성이 저장된 객체는 원래 원시데이터가 되기 때문에 값이 존재하지 않게 됩니다. 그러면서 str.prop를 콘솔로그 찍으면 'undefined'가 나타나게 됩니다.  
하지만 문자열과 관련해서 필요한 기능성을 객체지향적으로 제공해야하는 필요 또한 있기 때문에 `원시 데이터형을 객체처럼 다룰 수 있도록 하기 위한 객체`를 자바스크립트는 제공하고 있는데 그것이 `래퍼 객체(Wrapper Object)`입니다.