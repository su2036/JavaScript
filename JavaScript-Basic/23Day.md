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

- 예제, 극단적인 배열 랜덤 선택 예제

```js
let arr = new Array('seoul','new york','ladarkh','pusan', 'Tsukuba');
function getRandomValueFromArray(arr){
    let index = Math.floor(arr.length*Math.random());
    return arr[index];
}
console.log(getRandomValueFromArray(arr));
```

- 결과  
<img width="469" alt="스크린샷 2020-02-23 오후 9 13 00" src="https://user-images.githubusercontent.com/29330085/75111827-65635500-5681-11ea-9bbb-25aadb20b9d7.png">


> 배열`Array('seoul','new york','ladarkh','pusan', 'Tsukuba');`의 0,1,2,3,4값을 가져오기위해 index를 만들고 랜덤한 값을 출력시키기 위해 `Math.random`을 이용하고 'Math.random'은 `소수점`까지 나오게 되며 배열의 값의 수(0,1,2,3,4)를 곱하여 랜덤하게 출력시키괴 됩니다.   
추가로 `Math.floor메서드를 이용해서 소수점 전까지의 정수만 출력`시키게 사용합니다.

## 배열의 확장 2

- 예제, 내장객체를 prototype을 이용해 확장
```js
Array.prototype.random = function(){
    let index = Math.floor(this.length*Math.random());  // this -> arr를 가르킴, 배열 객체
    return this[index];
}
let arr = new Array('seoul','new york','ladarkh','pusan', 'Tsukuba');
console.log(arr.random());
```
- 결과  
<img width="472" alt="스크린샷 2020-02-23 오후 9 28 30" src="https://user-images.githubusercontent.com/29330085/75112056-7614ca80-5683-11ea-9ea9-ae80f8f7aeec.png">
  

> new Array로 객체를 만들때 `Array.prototype`안에 `.random`이라는 원형에 메서드를 추가하는 것입니다.
`console.log(arr.random());`을 통해서 `this`에 접근해서 index값을 랜덤하게 만들고 `return this[index];`로 결과 값을 받아옵니다.