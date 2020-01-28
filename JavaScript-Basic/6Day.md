# 반복문
## 반복문의 효용성

- 반복문이 없다면...?!?!

```html
<html>
<head>
</head>
<body>
<script type = "text/javascript">
    document.write("coding everybody 1<br />");
    document.write("coding everybody 2<br />");
    document.write("coding everybody 3<br />");
    document.write("coding everybody 4<br />");
    document.write("coding everybody 5<br />");
    document.write("coding everybody 6<br />");
    document.write("coding everybody 7<br />");
    document.write("coding everybody 8<br />");
    document.write("coding everybody 9<br />");
    document.write("coding everybody 10<br />");
</script>
</body>
```
> 이렇게 일일히 작성을 해야되는 안타까운 상황이 발생합니다.


- 반복문 사용!!

```html
<html>
<head>
</head>
<body>
<script type = "text/javascript">
    for(let i = 0; i<10; i = i + 1){
        document.write("coding every body" + (i+1) + "<br />");
    }
</script>
</body>
```
> 이렇게 반복문을 이용해서 1부터 10까지 출력이 되도록 작성이 가능합니다.  
0 부터 출력하는게 아닌 1부터 출력하기 위해서 `document.write("coding every body" + (i+1) + "<br />");`의 `(i+1)`을 통해 처음 반복문을 실행할 때 부터 0에서 1을 더해 1로 출력하게 됩니다.

## 반복문의 제어

- break
> 반복작업을 중간에 중단시키고 싶을때 `break`를 사용하면 됩니다.

```html
<html>
<head>
</head>
<body>
<script type = "text/javascript">
    for(let i = 0; i<10; i = i + 1){
        if(i === 5){
            break;
        }
        document.write(i + "<br />");   // 0,1,2,3,4
    }
</script>
</body>
```
> 코드 결과로는 0~4까지만 출력시키고 5가 나오는 순서부터는 출력되지않고 종료되버립니다.  


- continue
> 그 순간에만 종료되고 계속해서 반복문이 실행됩니다.

```html
<html>
<head>
</head>
<body>
<script type = "text/javascript">
    for(let i = 0; i<10; i = i + 1){
        if(i === 5){
            continue;
        }
        document.write(i + "<br />");   // 0,1,2,3,4,6,7,8,9
    }
</script>
</body>
```
> 코드 결과로는 0~4, 6~9까지 출력 되는 것을 확인할 수 있으며, continue는 break와 다르게 종료되지 않고 `5`가 되는 순간만 종료되고 그 뒤론 나머지 반복문을 실행 시키게 됩니다.  


## 반복문의 중첩사용과 디버거


```html
<html>
<head>
</head>
<body>
<script type = "text/javascript">
    for(let i = 0; i<10; i = i + 1){
        for(let j = 0; j<10; j = j + 1){
            document.write("coding everybody" + i + j + "<br />");   // 00,01,02,03,04,06,07,08,09,10,11,~ 99   
        }
    }
</script>
</body>
```
> 코드 결과를 보면 `00,01,02,03,04,06,07,08,09,10,11,~99`
로 출력 된것을 볼 수 있습니다.  
이렇게 반복문 안에 반복문을 실행할 수 있으며, `document.write("coding everybody" + i + j + "<br />");` 이 코드에서
"문자" + 숫자 + 숫자 + "문자"형식을 볼 수 있습니다.  
이 경우 자바스크립트는 숫자를 문자로 인식해줍니다.

Cf) 크롬 개발자 도구에서 Sources 탭에서 해당 코드 라인에 브레이크포인트를 걸 수 있으며 라인 하나하나를 실행하며 과정을 볼 수 있습니다.