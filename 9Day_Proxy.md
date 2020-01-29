# PROXY
> `Proxy`객체는 기본적인 동작(속성 접근, 할당 순회, 열거, 함수 호출 등)의 새로운 행동을 정의할 때 사용합니다.

어떤 오브젝트가 있을때 그 오브젝트를 가로채서 다른작업이 가능하게 해줍니다.

- 문법
```javascript
const p = new Proxy(target, handler);
```
> 이런식으로 쓰이며 

- 예재, Proxy를 써보자
```javascript
const myObj = {name:'changsu'};
const proxy = new Proxy(myObj, {}); // 타겟 오브젝트와 핸들러를 넣음, myObj에는 Proxy로 래핑할 대상 객체를 지정

proxy.name;                 // "changsu", 프로퍼티 접근

proxy.name = "jisu";        // jisu로 프로퍼티 값 할당

proxy.name;                 // "jisu"

toString.call(proxy);       // "[object Object]"

proxy;                      // Proxy {name: "jisu"}

myObj;                      // {name: "jisu"}

proxy === myObj;            // false

proxy == myObj;             // false
proxy.name == myObj.name;   // true
```

- 결과  
![스크린샷 2020-01-29 오전 4 04 51](https://user-images.githubusercontent.com/29330085/73296274-bf245b00-424c-11ea-817e-4af08e83de2f.png)


- 예제, handler `SET`과 `GET`, SET
```javascript
const myObj = {name : 'changsu'};
const proxy = new Proxy(myObj, {
    get : function() {
    },
    set : function() {
        console.log('change value');
    }
});

proxy.name;

proxy.name = "codesquad";
```
- 결과   
![스크린샷 2020-01-29 오전 9 05 57](https://user-images.githubusercontent.com/29330085/73316718-30790380-4277-11ea-8c9a-6df98c6b695d.png)
> codesquad로 변경할때 set함수change value가 바로 자동으로 불려지는 것을 확인 할 수 있습니다.   
값을 가로채 어떤 추가적인 작업이 가능합니다.

- 예제, handler `SET`과 `GET`, GET
```javascript
const myObj = {name : 'changsu'};
const proxy = new Proxy(myObj, {
    get : function() {
    },
    set : function() {
        console.log('change value');
    }
});

proxy.name;

proxy.name = "codesquad";
```









