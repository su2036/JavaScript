# Arguments
## arguments소개
> Arguments, 객체는 함수 안에서 함수의 여러가지 정보를 담고있는(특히 인자) 객체
사용방법이 배열과 유사하기 때문에 `유사배열`이라고도 합니다.

- 개념
```js
function a(arg1){   // arg1 은 a의 매개변수(parameter)
    ...
}
a(1)    // 1은 인자.
```

- 예시 
```js
function sum(){     // 매개변수가 없음
    let i, _sum = 0;    // i, for문을 위함
    for(i = 0; i < arguments.length; i++){  // arguments 특수변수명, 유사배열  = 인자가 들어있음(4)
        document.write(i+' : '+arguments[i]+'<br />');  // 첫번째로 전달된 1 = [i]
        _sum += arguments[i];   
    }   
    return _sum;
}
document.write('result : ' + sum(1,2,3,4));     // 인자 1,2,3,4 전달
```
- 결과  
<img width="100" alt="스크린샷 2020-02-16 오후 1 48 06" src="https://user-images.githubusercontent.com/29330085/74599321-31a58f80-50c3-11ea-8504-12c4bd27b72c.png">

> 1,2,3,4 인자를 전달하고 `arguments`에 1,2,3,4가 들어가면서 `.length`로 길이 4가 됩니다. 즉, 그리하여 for문에 i는 0~3까지 loop를 돌며 `argumnets[i]`에는 전달받은 인자 1,2,3,4를 순차적으로 i와 함께 document.write를 해서 보여주게 됩니다.
그리고 `_sum += arguments[i]`는 인자 1,2,3,4를 하나씩 더하고 값을 더해서 리턴하면 인자로 전달된 값에 대한 총합을 구하는 함수 결과를 보여주게 됩니다.





## 매개변수의 수 - function length
> 매개변수와 관련된 두가지 수가 있습니다.   
하나는 `함수 .length`, 다른 하나는 `arguments.length`입니다.   
함수 length는 함수로 `전달된 실제 인자의 수`를 의미하고, arguments.length는 함수에 `정의된 인자의 수`를 의미합니다.

- 예제1
```js
function zero(){    // 매겨변수 정의안함.
    console.log(
        'zero.length', zero.length,
        'arguments', arguments.length
    );
} 
zero();     // 인자도 전달 안함, zero.length 0 arguments 0 
```

- 예제2
```js
function one(arg1){ // 매개변수 하나 정의
    console.log(
        'one.length', one.length,   // 1, 정의된 매개변수 대로 받은 인자 1개 길이를 나타냄
        'arguments', arguments.length   // 2, 몇개의 인자를 전달했는지 길이를 나타냄
    );
}
one('val1', 'val2');    // 인자 두개 전달, one.length 1 arguments 2 
```

- 예제3
```js
function two(arg1, arg2){
    console.log(
        'two.length', two.length,   // 2, 정의된 매개변수 대로 받은 인자 2개 길이를 나타냄
        'arguments', arguments.length   // 1, 실제로 전달받은 인자의 길이를 나타냄
    );
}
two('val1');  // two.length 2 arguments 1
```

# 함수지향 - 함수의 호출
## apply소개

- 기본문법
```js
function func(){

}
func();
```

- 예제
```js
function sum(arg1, arg2){
    return arg1+arg2;
}
alert(sum.apply(null, [1,2]))   // 1+2 = 3
```

## apply사용

```js
o1 = {val1:1, val2:2, val3:3}
o2 = {v1:10, v2:50, v3:100, v4:25}

function sum(){
    var _sum = 0;       // _sum 0으로 초기화
    for(name in this){  // this라는 객체에 담겨있는 값을 for in문을 함수 호출할 때 정의됨
        _sum += this[name];
    }
    return _sum;
}
alert(sum.apply(o1))    //6, 1+2+3 
alert(sum.apply(o2))    //185, 10+50+100+25
```
