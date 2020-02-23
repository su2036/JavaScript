# 객체지향 - 표준 내장객체의 확장
## 표준 내장 객체란?
> 표준 내장 객체(Standard)는 자바스크립트가 기본적으로 가지고 있는 객체들을 의미합니다.  
내장 객체가 중요한 이유는 프로그래밍을 하는데 기본적으로 필요한 도구들이기 때문입니다.  
결국 프로그래밍이라는 것은 언어와 호스트 환경에 제공하는 기능들을 통해서 새로운 소프트웨어를 만들어내는 것이기 때문에 내장 객체에 대한 이해는 프로그래밍의 기본이라고 할 수 있습니다.

- 자바스크립트 내장 객체
  - Object  
  - Fucntion
  - Array
  - String
  - Boolean
  - Number
  - Math
  - Date
  - RegExp(정규표현식)

## 배열의 확장 1
- 예제
```js
let arr = new Array('seoul','new york','ladarkh','pusan', 'Tsukuba');
function getRandomValueFromArray(arr){
    let index = arr.length*Math.random()
    return result;
}
```

## 배열의 확장 2

