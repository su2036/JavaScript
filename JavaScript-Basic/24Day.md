# 객체지향 - Object
## Object란?
> Object 객체는 객체의 가장 기본적인 형태를 가지고 있는 객체입니다. 다시 말해서 아무것도 상속받지 않은 순수한 객체 입니다. 자바스크립트에서는 값을 저장하는 기본적인 단위로 Object를 사용합니다.
```js
let grades = {'changsu' : 10, 'egoing' : 6, 'sorialgi' : 80};   // 객체를 만들고 변수에 저장
```
동시에 자바스크립트의 모든 객체는 Object 객체를 상속 받는데, 그런 이유로 모든 객체는 Object 객체의 프로퍼티를 가지고 있습니다. 또한 Object 객체를 확장하면 모든 객체가 접근할 수 있는 API를 만들 수 있습니다.

## Object API 사용법
[MDN - Object 참고링크](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object)

```js
//Object.keys()
let arr = ["a", "b", "c"];
console.log('Object.keys(arr)', Object.keys(arr));  // Object.keys(arr) ["0","1","2"]

//Object.prototype.toString()
let o = new Object();   // Object.prototype.toSting 
console.log('o.toString()', o.toString());  // o = Object를 통해 만들어지기에 [Object Object]

let a = new Array(1,2,3);   // Object를 부모로 Array를 통해 만들어진 객체(1,2,3)
console.log('a.toString()', a.toString());  // 1,2,3
```
- 결과  
![스크린샷 2020-02-24 오후 11 27 36](https://user-images.githubusercontent.com/29330085/75160646-bea0b680-575d-11ea-8948-feb8e755346d.png)
  

- [Object.keys()사용법 - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) : `인자를 받아` 객체의 키 값만 수집해서 배열로 만들어 리턴 해주는 메서드입니다.

- [Object.prototype.toString()사용법 - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/toString) : 객체가 담고있는 어떠한 값이 무엇인지 문자열로 리턴해주는 것입니다.
  
  
## Object 확장
- 예제, Object를 확장시켜 모든 객체가 사용하게 메서드를 만듬, 설명을 위한 예제이며 이렇게 사용시 위험!
```js
Object.prototype.contain = function(checkvalue){    // 전달될 인자들을 checkvalue로 정의
    for(let name in this){  // for in 문을 이용해 메서드 안에 this는 메서드 안에 소속된 객체를 가져옴(o, a), name에는 각각의 키값이 전달됨
        if(this[name] === checkvalue){  // 반복문이 현재 차례의 값을 가져올때의 this와 가져온 인자(checkvalue)와 비교
            return true;    // 메서드 실행 종료
        }
    }
    return false    // 찾을 수 없으면 false 반환
} 

let o = {'name' : 'changsu', 'city' : 'seoul'}
console.log(o.contain('changsu'));  // 객체 o 안에 'changsu'가 있다면 true or false

let a = ['changsu','egoing','leezche'];
console.log(a.contain('egoing'));
```
> 객체에 어떠한 기능을 넣고싶을때 `prototype`을 이용하여 contain에 담고 메서드를 실행하게됩니다.
for in문을 이용해 메서드 안에 소속된 객체(o, a)를 가져오고 `name`에 각각의 키값이 전달 되게 됩니다.
if로 반복문이 돌면서 각각의 키 값을 가져온 값과 checkvalue로 가져온 인자와 같은지 비교를 하고   
`o.contain('changsu')`를 통해 비교한 값이 같기 떄문에 true를 반환하면서 메서드가 종료되게 됩니다.
즉, if로 인해 비교결과 같은 값이 아니라면 false를 반환하면서 종료되게 됩니다.

## Object 확장의 위험
- 예제, 위험한 이유는 모든 객체에 영향을 주기때문에 문제!
```js
Object.prototype.contain = function(checkvalue){    // 전달될 인자들을 checkvalue로 정의
    for(let name in this){  // for in 문을 이용해 메서드 안에 this는 메서드 안에 소속된 객체를 가져옴(o, a), name에는 각각의 키값이 전달됨
        if(this[name] === checkvalue){  // 반복문이 현재 차례의 값을 가져올때의 this와 가져온 인자(checkvalue)와 비교
            return true;    // 메서드 실행 종료
        }
    }
    return false    // 찾을 수 없으면 false 반환
} 

let o = {'name' : 'changsu', 'city' : 'seoul'}  // o 객체의 프로퍼티
let a = ['changsu','egoing','leezche']; // a 객체의 프로퍼티

for(let name in o){     // a
            console.log(name);
}
```
- 결과   
![스크린샷 2020-02-25 오후 10 59 33](https://user-images.githubusercontent.com/29330085/75255229-ef97ee80-5824-11ea-8267-6c320f88b67b.png)
![스크린샷 2020-02-25 오후 11 02 23](https://user-images.githubusercontent.com/29330085/75255242-f32b7580-5824-11ea-9857-68ceb5392e88.png)
>

- 예제, 위 코드 고치기!
```js
Object.prototype.contain = function(checkvalue){    // 전달될 인자들을 checkvalue로 정의
    for(let name in this){  // for in 문을 이용해 메서드 안에 this는 메서드 안에 소속된 객체를 가져옴(o, a), name에는 각각의 키값이 전달됨
        if(this[name] === checkvalue){  // 반복문이 현재 차례의 값을 가져올때의 this와 가져온 인자(checkvalue)와 비교
            return true;    // 메서드 실행 종료
        }
    }
    return false    // 찾을 수 없으면 false 반환
} 

let o = {'name' : 'changsu', 'city' : 'seoul'}  // o 객체의 프로퍼티
let a = ['changsu','egoing','leezche']; // a 객체의 프로퍼티

for(let name in a){
            if(a.hasOwnProperty(name)){     // name에 해당하는 프로퍼티를 어떠한 객체가 가지고 있는지 체크
                console.log(name);
            }  
}
```
- 결과  
![스크린샷 2020-02-25 오후 11 23 38](https://user-images.githubusercontent.com/29330085/75255936-14409600-5826-11ea-8a5a-5cc52d5aa88f.png)
![스크린샷 2020-02-25 오후 11 24 49](https://user-images.githubusercontent.com/29330085/75255939-160a5980-5826-11ea-85c7-ae25a17cb65c.png)  

> `hasOwnProperty()`를 이용해 메소드는 객체가 특정 프로퍼티를 가지고 있는지 나타내는 boolen값을 반환합니다. 그렇기 때문에 if를 사용하게 됩니다. 
호출하게되면 a 객체에 인자(name)로 전달한 값을 자신의 프로퍼티로 전달 하게 되도록 `hasOwnProperty`를 사용합니다.   
contain은 부모로 부터 상속 받은 프로퍼티이기 때문에 for in문을 통해서 열거가 되기 때문에 기존 확장했던 기존 위 코드는 객체 o와 a의 결과와 같이 contain의 결과도 반환되게 됩니다. 