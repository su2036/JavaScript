# 모듈
> 프로그램은 작고 단순한 것에서 크고 복잡한 것으로 진화됩니다.  
그 과정에서 `코드의 재활용성을 높이고, 유지보수를 쉽게` 할 수 있는 다양한 기법들이 사용됩니다.  

- 자주 사용되는 코드를 별도의 파일로 만들어서 필요할 때마다 재활용할 수 있습니다.
- 코드를 개선하면 이를 사용하고 있는 모든 애플리케이션의 동작이 개선됩니다.
- 코드 수정 시에 필요한 로직을 빠르게 찾을 수 있습니다.
- 필요한 로직만을 로드해서 메모리의 낭비를 줄일 수 있습니다.
- 한번 다운로드된 모듈은 웹브라우저에 의해서 저장되기 떄문에 동일한 로직을 로드 할 때 시간과 네트워크 트래픽을 절약할 수 있습니다.

## 모듈이란?
> 순수한 자바스크립트에서는 모듈(module)이라는 개념이 분명하게 존재하지 않습니다. 하지만 자바스크립트가 구동되는 호스트 환경에 따라서 서로 다른 모듈화 방법이 제공되고 있습니다.

## 모듈화
- 모듈이 없다면?
```html
<html>
<head>
    <meta charset="utf-8"/>
</head>
<body>
    <script>
        function welcom(){
            return 'hello world';
        }
        alert(welcome());
    </script>
</body>
</html>
```

- 모듈 사용

```html
<html>
<head>
    <meta charset="utf-8"/>
    <script src="greeting.js"></script>
</head>
<body>
    <script>
        alert(welcome());
    </script>
</body>
</html>
```
  - greeting.js
```javascript
function welcom(){
    return 'hello world';
}
```

## Node.js의 모듈화
> 호스트 환경에 따라 모듈을 로드하는 방법이 달라진 다는 것을 확인해보겠습니다.

- node.circle.js(로드될 대상) = 위에서 greeting.js와 동일
```js
let PI = Math.PI;

exports. area = function (r) {
    return PI * r * r;
};

exports.circumference = function (r) {
    return 2 * PI * r;
}
```

- node.demo.js(로드의 주체) = 위에서 html과 동일
```js
let circle = require('./node.circle.js');

console.log('The area of a circle of radius 4 is') + circle.area(4));
```
> node.demo.js를 `node node.demo.js`명령으로 실행하게 되면 'node.circle.js'를 인클루드해서 실행됩니다.


## 라이브러리
모듈 = 프로그램을 구성하는 작은 부품, 라이브러리 = 자주 사용되는 로직을 `재사용하기 편리하도록 잘 정리한 코드들의 집합`

- `jquery`사용  
[Jquery홈페이지](https://jquery.com/)

## 라이브러리 사용하기
```html
<!--jqery.demo.html-->
<html>
<head>
    <meta charset="utf-8"/>
    <script type="text/javascript" src="jquery-3.4.1.min.js"></script>
</head>
<body>
    <ul id = "list">
        <li>empty</li>
        <li>empty</li>
        <li>empty</li>
        <li>empty</li>
        <li>empty</li>
    </ul>
    <input type="button" value="execute" id="execute_btn" />
    <script type="text/javascript">
        $('#execute_btn').click(function(){         // execute라는 버튼을 눌렀을때!
            $('#list li').text('coding everybody'); // coding everybody로 li태그 안 텍스트 변경
        })
    </script>
</body>
</html>
```
- 결과  
![스크린샷 2020-02-04 오전 7 38 21](https://user-images.githubusercontent.com/29330085/73697277-80494600-4721-11ea-9e3a-cb0f001470a4.png)
![스크린샷 2020-02-04 오전 7 38 31](https://user-images.githubusercontent.com/29330085/73697276-7fb0af80-4721-11ea-8308-c2e86c266052.png)


