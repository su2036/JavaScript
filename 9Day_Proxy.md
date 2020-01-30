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

proxy.name;                 // get할땐 undefined

proxy.name = "codesquad";   // change value "codesquad"
```
- 결과   
![스크린샷 2020-01-29 오전 9 05 57](https://user-images.githubusercontent.com/29330085/73316718-30790380-4277-11ea-8c9a-6df98c6b695d.png)
> codesquad로 변경할때 set함수change value가 바로 자동으로 불려지는 것을 확인 할 수 있습니다.   
값을 가로채 어떤 추가적인 작업이 가능합니다.

- 예제, handler `SET`과 `GET`, GET
```javascript
const myObj = {name : 'changsu'};
const proxy = new Proxy(myObj, {
    get : function(target, property, receiver) {
        console.log('get value');
        return target [property];
    },
    set : function() {
        console.log('set value');
    }
});

proxy.name;                 // get value "changsu"

proxy.name = "codesquad";   // set value "codesquad"

proxy.name;                 // get value "changsu"
```
- 결과  
![스크린샷 2020-01-30 오전 9 00 51](https://user-images.githubusercontent.com/29330085/73408363-57027180-433f-11ea-9459-1452df774870.png)  
> get value인 "changsu"가 proxy.name; 실행 시 출력되고, proxy.name에 "codesquad"를 할당하게되면 set value라는 값을 출력해주면서 사용 되는 것을 확인 할 수 있습니다.

- proxy, get과 set에 추가적인 작업을 하기
```javascript
const myObj = {name : 'changsu'};
const proxy = new Proxy(myObj, {
    get : function(target, property, receiver) {    // target은 Proxy의 첫번째 인자 myObj
        console.log('get value');
        return target [property];
    },
    set : function(target, property, value) {
        console.log('set value');
        target[property] = value;
    }
});

proxy.name;

proxy.name = "codesquad";

proxy.name;
```

- 결과  
![스크린샷 2020-01-30 오전 9 18 55](https://user-images.githubusercontent.com/29330085/73409106-a47fde00-4341-11ea-8ee1-ba5fc586277f.png)
> 위 결과와 같이 "codesquad"를 할당하는 추가적인 작업이 가능합니다.

- 변경한 횟수도 알아보자!!
```javascript
const myObj = {name : 'changsu', changedValue : 0};
const proxy = new Proxy(myObj, {
    get : function(target, property, receiver) {    // target은 Proxy의 첫번째 인자 myObj
        console.log('get value');
        return target [property];
    },
    set : function(target, property, value) {
        console.log('set value');
        target['changedValue']++;       // 
        target[property] = value;
    }
});
```
- 결과  
![스크린샷 2020-01-30 오전 9 28 28](https://user-images.githubusercontent.com/29330085/73409518-e3626380-4342-11ea-8775-2568eb95576d.png)
> 프록시를 통해서 get과 set을 이용해서 중간에 가로챈 값을 변경하고 변경한 횟수가 몇번인지 알수 있습니다.



```javascript
    const proxy = new Proxy({name : 'changsu', changedValue : 0}, { })
```
> proxy를 통해서만 name값을 변경 가능합니다.


- Reflect(오브젝트안에 값을 뽑아내기), 값을 반환
```javascript
const proxy = new Proxy({name : 'changsu', changedValue : 0}, {
    get : function(target, property, receiver) {    // target은 Proxy의 첫번째 인자 myObj
        console.log('get value');
        return Reflect.get(target,property);
    },
    set : function(target, property, value) {
        console.log('set value');
        target['changedValue']++;       // 
        target[property] = value;
    }
});

proxy.name = "changsubae";
proxy.name = "codesquad";   
proxy.changedValue;         // set value  set value 2
proxy.name;                 // codesquad
```

- 결과  
![스크린샷 2020-01-30 오전 9 32 19](https://user-images.githubusercontent.com/29330085/73409733-769b9900-4343-11ea-8294-9edac83294ed.png)





