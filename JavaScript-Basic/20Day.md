# 객체지향 - 생성자와 new
## 자바스크립트의 객체지향
### 객체 
> 객체란 서로 연관된 변수와 함수를 그룹핑한 그릇이라고 할 수 있습니다. 객체 내의 `변수를 프로퍼티(property)`,`함수를 메소드(method)`라고 부릅니다.

## 객체 생성
- 예제, 기본 문법
```js
let person = {} //{object} => 객체
person.name = 'changsu';    // 객체에 담겨있는 변수(프로퍼티) : name
person.introduce = function(){  // 객체내에 담겨있는 함수(메소드) : introduce
    return 'My name is '+ this.name;    // this : 함수가 담고 있는 객체(person)를 가르킴
}
document.write(person.iuntroduce());    // My name is Changsu
```

- 예제, 객체 내에 직접 정의
```js
let person = {
    'name' : 'changsu',
    'introduce' : function(){
        return 'My name is ' + this.name;
    }
}
document.write(person.introduce());
```

## 생성자와 new
> 생성자(constructor)는 객체를 만드는 역할을 하는 함수입니다. 자바스크립트에서 함수는 재사용 가능한 로직의 묶음이 아니라 객체를 만드는 창조자라고 할 수 있습니다.

```js
function Person(){}
let p = new Person();   // p 에는 함수 Person()에 new를 부쳐서 Person{} 비어있는 객체를 생성
p.name = 'changsu';
p.introduce = function(){   // introduce프로퍼티는 메소드가 됨
    return 'My name is '+ this.name;
}
```

- 예제, 이름을 두개 출력시키면서 중복되는 것을 해결할 때
```js
function Person(name){      // Person이라는 함수를 정의함. 초기화
    
    this.name = name;
    this.introduce = function(){    // 한번만 메소드를 쓸수 있음
        return 'My name is '+ this.name;
    }
}
let p1 = new Person('changsu'); // 생성자로 'changsu' name을 향하면서 프로퍼티가 됨, 위 코드를 통해 p1변수에 담기게 됨
document.write(p1.introduce()+"<br />");

let p2 = new Person('tester');
document.write(p2.introduce()+"<br />");
```

- 결과  
![스크린샷 2020-02-19 오전 8 58 26](https://user-images.githubusercontent.com/29330085/74788771-09ea3d80-52f6-11ea-98d9-744a313b282c.png)  

> 함수 Person에 객체 name과 introduce 객체 메소드를 확인할 수 있으며 밑에 p1과 p2라는 변수에 각각 생성자 함수를 이용해 전달할 문자열이 있으며 이 문자열들은 각각 Person(name)에 전달되며 실행될때 초기화를 통해 변수 p1,p2를 각각 리턴하여 결과가 나오게 됩니다.