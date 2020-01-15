# 조건문
> 조건문이란, 주어진 조건에 따라서 애플리케이션을 다르게 동작하도록 하는 것입니다.

## 조건문의 문법
# IF
> 조건문은 `if`로 시작합니다. if뒤에 괄호에 조건이 오고, 조건이 될 수 있는 값은 `Boolean`입니다.  
Boolean의 값이 true라면 조건이 담겨진 괄호 다음의 중괄호 구문이 실행됩니다.

- 예제, if뒤에 true.
    ```javascript
    if(true){
        alert('result : true'); // 실행이 되서 'result : true'라는 경고창이 뜹니다.
    }
    ```
- 예제, if뒤에 false.
    ```javascript
    if(false){
        alert('result : true'); // 실행이 되지 않습니다.
    }
    ```
    > if에 `true`가 온것은 실행이 되고 `false`가 온것은 실행이 되지 않습니다.
    여기서 조건문이 `boolean`이라는 데이터 타입은 땔래야 땔수 없는 이유입니다.

- 예제, 좀 더 생각을 해볼까요?
    ```javascript
    if(true){
        alert('1');     // true로 경고창에 1이 실행 된 것을 확인할 수 있으며 확인을 눌러야
        alert('2');     // 다음 2가 경고창에 실행됩니다.
        alert('3');
        alert('4');     // 똑같이 여기까지 경고창에 4가 실행 된디 확인을 누르게되면
    }
    alert('5');         // if 조건문이 다 실행 된 뒤, 즉 4다음으로 경고창에 5가 나타나게 됩니다.
    ```

    ```javascript
    if(false){
        alert('1');     // false로 '{}' 중괄호 안에 내용이 실행 되지 않습니다.
        alert('2');
        alert('3');
        alert('4');
    }
    alert('5');         // if조건문이 실행되지 않고 바로 '{}'중괄호 밖인 alert(5)가 실행 되게 됩니다.
    ```
    > 위 코드처럼 실행 되는 이유는 if조건문이 true(참)이면 `{}중괄호`안에 코드가 실행 되고, false(거짓)이면 `{}중괄호`안에 코드가 실행 되지 않기 때문에 if(false)코드는 실행했을 때 바로 경고창에 5가 확인 됩니다.

## ELSE
> else, if만으로 좀 더 복잡한 상황을 처리하는데 부족할때.
- 문법
```javascript
if(true){
    alert(1);   // 실행.
}else{
    alert(2);   // 실행 안됨.
}
```
> if(true)이기 떄문에 `{}중괄호 안`에 있는 `alert(1)`만 실행됩니다.

```javascript
if(false){
    alert(1);   // 실행 안됨
}else{
    alert(2);   // 실행
}
```
> if(false)이기 때문에 `{}중괄호 안`에 있는 `alert(1)`은 실행 되지 않고 `else 안`에 `alert(2)`만 실행됩니다.

## ELSE IF
> else if를 이용하면 조건문을 좀 더 풍부하게 할 수 있습니다.
- 예제1,
    ```javascript
    if(false){
        alert(1);
    }else if(true){     // 실행
        alert(2);
    }else if(true){     // 실행 안됨
        alert(3);
    }else{
        alert(4);
    }
    ```
    > 결과는 2입니다.
- 예제2,
    ```javascript
    if(false){
        alert(1);
    }else if(false){    // 실행 안됨
        alert(2);
    }else if(true){     // 실행
        alert(3);
    }else{
        alert(4);
    }
    ```
    > 결과는 3입니다.


## 조건문의 응용
### 변수와 비연산자
- 예제
    ```html
    <HTML>
        <head>
            <meta charset="utf-8"/>
        </head>
        <body>
            <script>
                var id = prompt('ID를 입력하시오.');
                if(id =='changsu'){
                    var pw = prompt('PW를 입력하시오.');
                    if(pw == '1234'){
                        alert('로그인 하셨습니다.' + id + '님 환영합니다.');
                    }else{
                        alert('PW가 틀렸습니다.');
                    }
                }else{
                    alert('ID가 일치하지 않습니다.');
                }
            </script>
        </body>
    </HTML>
    ```
- 결과  
    ![스크린샷 2020-01-16 오전 7 44 11](https://user-images.githubusercontent.com/29330085/72477959-2b0dc900-3834-11ea-85cf-4de898c05b39.png)  

    ![스크린샷 2020-01-16 오전 7 54 02](https://user-images.githubusercontent.com/29330085/72478476-74124d00-3835-11ea-80d7-38c82a432cd4.png)  

    ![스크린샷 2020-01-16 오전 7 55 01](https://user-images.githubusercontent.com/29330085/72478511-84c2c300-3835-11ea-9c71-b29e5c63381e.png)  
    
    ![스크린샷 2020-01-16 오전 7 55 34](https://user-images.githubusercontent.com/29330085/72478568-986e2980-3835-11ea-8779-1f985ef057d8.png)  

    ![스크린샷 2020-01-16 오전 7 56 07](https://user-images.githubusercontent.com/29330085/72478590-ac199000-3835-11ea-9b9b-efceeb3f49b6.png)  
    
## 논리 연산자
### &&
> &&는 좌항과 우항이 모두 true(참)일때 true(참)이 됩니다.
```javascript
if(true && true){   // 좌항과 우항이 true로 같고 결과는 true이기에 실행되어
    alert(4);       // 4가 뜨게 됩니다.
}

if(true && false){  // false로 실행 되지 않습니다.
    alert(3);
}

if(false && true){  // false로 실행 되지 않습니다.
    alert(2);
}

if(false && false){ // false로 실행 되지 않습니다.
    alert(1);
}
```

- 예제  

    ```html
    <HTML>
        <head>
            <meta charset="utf-8"/>
        </head>
        <body>
            <script>
                var id = prompt('ID를 입력하시오.');
                var pw = prompt('PW를 입력하시오.');
                if(id =='changsu' && pw == '1234'){
                    alert('로그인 하셨습니다.' + id + '님 환영합니다.');
                }else{
                    alert('로그인에 실패하셨습니다.');
                }
            </script>
        </body>
    </HTML>
    ```
    > `if(id =='changsu' && pw == '1234')`으로 위 코드를 수정 할 수 있습니다.  
    즉 id와 pw가 일치해야 로그인 되었다고 뜨게 되며, ID입력이 틀려도 PW입력이 가능하나   
    ID : changsu, PW : 1234 둘중에 하나라도 틀려도 '로그인에 실패하셨습니다.'가 뜨게 됩니다.  
    - 결과  
    ![스크린샷 2020-01-16 오전 8 25 50](https://user-images.githubusercontent.com/29330085/72480168-d4a38900-3839-11ea-8697-4f909fc0f580.png)


### ||
> ||는 좌항과 우항 중에 하나라도 true라면 ture가 되는 논리 연산자입니다. 또 둘다 false이면 false가 됩니다. 즉, `OR연산자`입니다.
- 예제
    ```javascript
    if(true || true){       // true로 실행 됨
        alert(1);
    }
    if(true || false){      // true로 실행 됨
        alert(2);
    }
    if(false || true){      // true로 실행 됨
        alert(3);
    }
    if(false || false){     // false로 실행 되지 않음
        alert(4);
    }
    ```

- 예제, &&와 ||를 동시에 사용
```html
<HTML>
        <head>
            <meta charset="utf-8"/>
        </head>
        <body>
            <script>
                var id = prompt('ID를 입력하시오.');
                var pw = prompt('PW를 입력하시오.');
                if((id =='changsu' || id == 'su2036' )&& pw == '1234'){
                    alert('로그인 하셨습니다.' + id + '님 환영합니다.');
                }else{
                    alert('로그인에 실패하셨습니다.');
                }
            </script>
        </body>
    </HTML>
```
- 결과  
![스크린샷 2020-01-16 오전 8 48 29](https://user-images.githubusercontent.com/29330085/72481189-09fda600-383d-11ea-94eb-c87aa41ce526.png)  
> if((id =='changsu' || id == 'su2036' )&& pw == '1234')로 ||가 오면서 ID가 'changsu', 'su2036' 둘중에 아무거나 쓰고 PW를 '1234'를 입력하면 로그인에 성공 하게 됩니다.  

### !
!는 부정의 의미로 `Boolean`의 값을 역전 시킵니다. 즉, `true를 false`로 `false를 true`로 역전시킵니다.
```javascript
if(!true && !true){     // false와 false 이기 떄문에 실행되지 않음
    alert(4);
}

if(!false && !true){    // true와 false이기 떄문에 실행되지 않음
    alert(3);
}

if(!true && !false){    // false와 true이기 떄문에 실행되지 않음
    alert(2);
}
if(!false && !false){   // true와 true이기 때문에 실행 됨
    alert(1);
}
```

## boolean의 대체제
### 0 1
> 조건문에 사용될 수 있는 데이터 형이 꼭 불린만 되는 것은 아닙니다. 관습적인 이유로   
`0은 false, 0이 아닌 값은 true로 간주`합니다.
```javascript
if(0){alert(1)}     // 0은 false이므로 실행 되지 않음

if(1){alert(2)}     // 1은 true이므로 실행됨
```

### 기타 false로 간주되는 데이터 형
> false와 0 외에 false로 간주되는 데이터형 리스트입니다. 조건문에 조건으로 !(부정)연산자를 사용하면 주어진 값은 false가 되기 떄문에 실행되지 않습니다.
```javascript
if(''){alert('빈문자열');}             // 빈문자열은 false로 실행 되지 않음

if('test'){alert('빈문자열')}          // 실행 됨

if(undefined){alert('undefined')}    // undefined는 false이기 떄문에 실행 되지 않음

var a;                               // 값이 할당되지 않아 undefined가 될것이고
if(!a){                              // !부정이 되어 부정에 반대로 True가 되어 실행 됩니다.
    alert('값이 할당되지 않은 변수');
}

if(!null){                          // null 또한 부정에서 !떄문에 True가 되어 실행됨 
    alert('null');
}

if(!NaN){                           // NaN도 부정에서 !떄문에 True가 되어 실행됨
    alert('NaN');                   
}
```