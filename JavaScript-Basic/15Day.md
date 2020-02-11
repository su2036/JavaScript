# 함수지향 - 값으로서의 함수와 콜백
## 함수의 용도 -1

### 값으로서의 함수
- 예제
```js
let a = value; 
```
> value라는 값을 변수 a에 담았습니다라는 뜻이고

- 예제
```js
function a(){}  
```
> let a = function(){}은 함수'function(){}'이 변수 a에 담기면서 값이 될 수 있습니다.

- 예제
```js
a = {
    b:function()}{
    }
};
```
> 객체의 값이 `함수'function(){}'`이 될 수 있으며, `b` 객체의 'Key'가 되며 `'function(){}'`은 'value'가 됩니다.  
이렇게 객체의 속성(b) 값(function())으로 담겨진 함수를 `메소드(method)`라고 불립니다. 즉, 객체안에 함수는 메소드입니다.


- 예제
```js
function cal(func, num){    // cal에 첫번째 인자로 전달된 func라는 함수를 두번째로 전달된 인자의 값인 num을 전달함
    return func(num)        // num함수 호출
}

function increass(num){
}
    return num+1
}

function decrease(num){
    return num-1
}

alert(cal(increase, 1));
alert(cal(decrease, 1));
```
> 함수는 값이기 떄문에 다른 함수의 인자로 전달 될수도 있습니다.
예제를 보면,
```js
function cal(func,num){
    let func = increase(num){
        return num+1
        }
        위 개념처럼 func(1) => func(1)은 num = 1이 되면서 1(num)+1이 리턴되어 1+1인 2라는 값이 되며 이런식으로 동작됩니다.
```
> 그리하여 alert(cal(increase, 1))의 결과는 2가 되게 되고, cal(decrease, 1)의 결과는 0이 되는 것을 확인 할 수 있습니다.


## 값으로서의 함수와 콜백 - 함수의 용도 -2

```js
function cal(mode){     // plus 또는 minus를 함
    let funcs = {
        'plus' : function(left, right){return left + right},    // 첫번쨰 인자 2 + 두번째 1
        'minus' : function(left, right){return left - right}    // 첫번쨰 인자 2 - 두번째 1
    }
    return funcs[mode];     // plus 또는 minus를 하게됨
}
alert(cal('pluse')(2, 1);   // 3
alert(cal('minus')(2, 1));  // 1
```
> 함수는 함수의 리턴 값으로도 사용할 수 있습니다.

```js
let process = [
    function(input){ return input + 10;},
    function(input){ return input * input;},
    function(input){ return input / 2;}
]
let input = 1;
for(let i = 0; i < process.length; i++){    // process의 길이보다 i값이 작은동안 
    input = process[i](input);              // i++ 한 0일때 함수 첫번째라인, 1일때 함수 두번쨰라인, 2일때 세번째 라인을 실행
}
alert(input);
```
- 결과  
![스크린샷 2020-02-11 오전 8 10 09](https://user-images.githubusercontent.com/29330085/74198887-f6135b80-4ca5-11ea-9476-e8c3ac83dbfc.png)
  

> `input에 1`을 넣어 실행 시작하기 때문에 함수 첫번째 라인`input + 10`인 1+10이 실행되고 결과인 11을 input에 저장하여  
다시 11을 input에 넣어 함수 두번째 라인인 `input*input`인 11*11이 되어 121이라는 값이 다시 input에 저장됩니다.   
그리고 다시 함수 세번째 라인인 `input / 2`인 121 / 2 가되어 결과로 경고창에 60.5가 나오게 됩니다.
배열의 값으로도 사용이 가능 합니다.

## 값으로서의 함수와 콜백 - 콜백이란?
```js
let numbers = [20, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1];
let sortfunc = function(a, b){
    console.log(a,b);
    if(a > b){
        return 1;   // 양수
    } else if (a < b){
        return -1;  // 음수
    } else {
        return 0;   // 0
    }
}
console.log(numbers.sort(sortfunc));
```

- 예제, 코드 줄이기
```js
let numbers = [20, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1];
let sortfunc = function(a,b){
    return b-a;
}
console.log(numbers.sort(sortfunc));    // 콜백 sortfunc
```
- 결과  
![스크린샷 2020-02-11 오전 8 48 06](https://user-images.githubusercontent.com/29330085/74200804-3c1eee00-4cab-11ea-9780-ebd7d13c5549.png)
![스크린샷 2020-02-11 오전 8 48 55](https://user-images.githubusercontent.com/29330085/74200840-5953bc80-4cab-11ea-97ba-a36830e624e2.png)
> 위 코드들을 보면 a, b 두개를 각각 양수인지 음수인지 0인지를 비교하여 순차적으로 또는 역순으로 결과를 나타 내게 됩니다.
여기서 `(numbers.sort(sortfunc));`해당 라인에 sortfunc가 콜백입니다.

## 비동기 콜백과 Ajax

### 비동기 처리
> 콜백은 비동기처리에서도 유용하게 사용됩니다. 시간이 오래걸리는 작업이 있을 때 이 작업이 완료된 후에 처리해야 할 일을 콜백으로 지정하면 해당 작업이 끝났을 때 미리 등록한 작업을 실행하도록 할 수 있습니다.

### Ajax
> Asynchronous Javascript and XML 줄임말.

- 예제, datasource.json.js
```js
{"title":"JavaScript","author":"changsu"}
```

- 예제, demo1.html
```html
<html>
<head>
    <script src = "//code.jquery.com/jquery-3.4.1.min.js"></script>
</head>
<body>
    <script type = "text/javascript">
    $.get('./datasource.json.js',   // 첫번째 인자로 데이터를 가져옴
        function(result){           // 서버와 통신 작업이 끝났을때 함수를 호출
            console.log(result);
        }, 'json');
    </script>
</body>
</html>
```
- 결과  
![스크린샷 2020-02-12 오전 8 26 27](https://user-images.githubusercontent.com/29330085/74289236-d34e7900-4d71-11ea-8e3a-fd98addd2433.png)
![스크린샷 2020-02-12 오전 8 25 43](https://user-images.githubusercontent.com/29330085/74289242-d6e20000-4d71-11ea-9b9d-8a613d6fa902.png)
> `$.get('./datasource.json.js', ` get의 첫번째 인자로 데이터를 가져오고  
`function(result){ ` 서버와 통신 작업이 끝났을때 함수를 호출하며 함수의 두번째 인자인 result(매개변수, 가져온 데이터를 객체로 만듬)를 호출 한다는 뜻입니다.