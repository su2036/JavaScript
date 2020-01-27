# 반복문
## 반복문 기본문법 - while
- while, for : ~하는 동안

- while 기본 문법
```javascript
while (조건) {
    반복해서 실행할 코드
}
```
> `()안에 있는 조건`이 `TRUE`인 동안에 반복해서 실행할 코드가 실행되고 `TRUE -> FALSE`가 될때 까지 돌아 갑니다.

- 예제코드
```html
<html>
    <head>
    </head>
    <body>
        <script type="text/javascript">
            while(true) {
                document.write("coding everybody <br />");
            }
        </script>
    </body>
</html>
```
> 해당 코드를 실행 시키게 되면 무한루프를 돌아서 웹 페이지가 죽게 됩니다.


## 반복 조건
> 반복문을 언제까지 실행 시킬 것인가?!! 중단 시켜보자!!

- 예제코드
```html
<html>
    <head>
    </head>
    <body>
        <script type="text/javascript">
            let i = 0;
            while(i < 10) {     // i가 10보다 작을 때 까지는 true 이기에 실행, 같거나 크다면 false가 됨
                document.write("coding everybody <br />");
                i= i + 1; 
            }
        </script>
    </body>
</html>
```
> 위 중단시키기 위한 조건을 `i < 10` 하게 되면서 `i= i + 1;`해당 코드로 인해 i에 1씩 더하게 됩니다.  
반복을 하면서 i가 9일때 까지 반복하고 10이되면 false로 반복을 중단하게 됩니다.

## for 문
- 기본 분법
```javascript
for(초기화; 반복조건; 반복이 될 때마다 실행되는 코드) {
    반복해서 실행될 코드
}
```

- 예제코드
```html
<html>
    <head>
    </head>
    <body>
        <script type="text/javascript">
            for(let i = 0; i < 10; i++) {
                document.write("Coding everybody <br />");
            }
        </script>
    </body>
</html>
```
> while문에서 따로 변수 초기화라인과 반복조건 라인, 그리고 반복 될 때마다 실행되는 코드 총 3라인을 for문에선 1라인으로 줄여 코딩이 가능합니다.  
`let i = 0;`은 초기화, `i < 10;`는 반복조건으로 true일때 실행되게 되며, `i++`는 반복이 될때마다 i에 값을 1씩 더한다가 되게 됩니다.  
i 값이 10이 되면 반복문을 벗어나 밑에 코드가 실행되게 됩니다.

<hr />



## 반복문의 효용성

## 반복문의 제어

## 반복문의 중첩사용과 디버거

