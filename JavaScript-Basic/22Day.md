# 상속
## 상속(inheritance)이란?
> 객체는 연관된 로직들로 이루어진 작은 프로그램이라고 할 수 있습니다.  
상속은 객체의 로깆을 그대로 물려 받는 또 다른 객체를 만들 수 있는 기능을 의미합니다.  
기존의 로직을 수정하고 변경해서 파생된 새로운 객체를 만들 수 있게 해줍니다.


- 예제
```js
function Person(name){  // Person 생성자
    this.name = name;   // name이라는 프로퍼티
    this.introduce = function(){    // 객체를 생성하는 객체
        return 'My name is ' + this.name;
    }
}
let p1 = new Person('changsu');
document.write(p1.introduce()+"<br />");    // My name is changsu
```

```js
function Person(name){  // Person 생성자
    this.name = name;
}

Person.prototype.name = null;   // 객체(함수) Person에 프로토타입이라는 프로퍼티가 있고 그안엔 어떤 객체가 들어있으며 .name으로 객체에게 어떤 값(null)을 줄수 있고
Person.prototype.introduce = function(){    // introduce, 함수를 할당하게 되면 그 객체안에 메소드를 정의하게 되는 것임
    return 'My name is '+this.name;
}
let p1 = new Person('changsu');
document.write(p1.introduce()+"<br />");    // My name is changsu, introduce 메소드 실행
```

> Person객체(함수)에 프로토타입이라는 프로퍼티가 있고 그안엔 어떤 객체가 들어있으며 .name으로 객체에게 어떤 값(null)을 전달해 줄 수 있습니다.   
`Person.prototype.introduce = function()` 함수를 할당하게 되면 그 객체안에 메소드를 정의하게 됩니다.  
즉, `return 'My name is '+this.name;`이 실행되게 됩니다.  
`p1.intruduce()를 통해 p1 = new Person('changsu')`로 인자를 전달해주게 되고 메소드를 실행함으로 name객체에 인자 'changsu'를 전달받으면서 결과를 볼 수 있습니다.

## 상속의 사용법
- 사용법 예제

```js
function Person(name){  // 사람이라는 생성자를 통해 만들어진 객체
    this.name = name;
}
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}
 
function Programmer(name){  // 프로그래머라는 생성자를 통해 객체를 만듬
    this.name = name;
}
Programmer.prototype = new Person();    // new Person()을 통해 Person()의 .prototype.name과 .prototype.introduce의 속성 프로퍼티와 메소드를 가져와 사용
 
let p1 = new Programmer('changsu');
document.write(p1.introduce()+"<br />");
```
> 프로그래머라는 생성자를 통해 만들어진 객체가 사람이라는 생성자를 통해 만들어진 객체의 동일한 기능성을 가지도록 상속받아 사용하는 내용입니다.  
`new Programmer`를 통해 프로그래머 생성자를 호출, new로 인해 객체를 만듭니다. 여기서 인자 'changsu'를 전달 하여 `name`이라는 값에 changsu가 담기게 됩니다.  
그리고 `p1.introduce()`는 Person의 객체에 `prototype.intruduce`메소드가 정의되어 있는데 여기서 `상속받아` 결과를 출력하게 됩니다.  
Programmer.prototype = new Person();을 통해 `Person.prototype이 갖고있는 .name이라는 프로퍼티와 .introduce메소드`를 마치 복사하여 가져오듯이 가지고 있는 객체가 prototype안에 들어가 있기 떄문에 new Person으로 만들어진 객체는 `.name과 .introduce`를 가지고 있는 객체가 Programmer`.prototype`이 되게 됩니다.
이렇게 되면 Programmer.prototype의 값이 `Person()`의 속성을 가저와 new를 통해 만들게 됩니다.  
그리고 `let p1 = new Programmer`를 해서 `function Programmer`객체화시키면서 Programmer`.prototype`의 속성과 값을 받아 결과를 보여주게 됩니다.

## 기능의 추가
- 예제

```js
function Person(name){
    this.name = name;
}
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}
 
function Programmer(name){
    this.name = name;
}
Programmer.prototype = new Person();
Programmer.prototype.coding = function(){
    return "hello world";
}
 
let p1 = new Programmer('changsu');
document.write(p1.introduce()+"<br />");
document.write(p1.coding()+"<br />");
```
> 실행하게 되면 `p1.introduce()`를 Programmer라는 생성자를 통해 정의한적이 없지만 Person에서의 .protyotype.introduce의 정의되어있는 메소드를 실행하게 됩니다.  
그리고 `p1.coding`은 Programmer에서의 `.prototype.coding의 메소드를 실행`하여 결과를 출력해주게 됩니다.  
즉, 프로그래머도 사람이기에 Person.prototype.introduce의 기능(이름)도 있고 `기능이 중복되기에 사람이라는 것에 기능을 상속`받아 쓰고 `.coding의 기능은 프로그래머만 쓰는 기능`이기에 Programmer.prototype.coding을 통해 메소드를 실행하여 결과를 내게 됩니다.

- 추가 예제 
```js
function Person(name){
    this.name = name;
}
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}
 
function Programmer(name){
    this.name = name;
}
Programmer.prototype = new Person();
Programmer.prototype.coding = function(){
    return "hello world!";
}

function Designer(name){
    this.name = name;
}
Programmer.prototype = new Person();
Programmer.prototype.design = function(){
    return "Design is beautiful!";
}

let p1 = new Programmer('changsu');
document.write(p1.introduce()+"<br />");
document.write(p1.coding()+"<br />");

let p1 = new Programmer('kyeongsik');
document.write(p1.introduce()+"<br />");
document.write(p1.design()+"<br />");
```
- 결과  
![스크린샷 2020-02-21 오전 8 57 43](https://user-images.githubusercontent.com/29330085/74991043-4188ef00-5488-11ea-930a-7e930ed5f872.png)
  

## prototype
> `객체의 원형`이라고 할 수 있습니다. 함수는 객체입니다. 그러므로 `생성자로 사용될 함수도 객체`입니다.  
객체는 프로퍼티를 가질 수 있는데 `prototype이라는 프로퍼티는 용도가 약속`되어 있는 특수한 프로퍼티 입니다.  
prototype에 저장된 속성들은 `생성자를 통해 객체가 만들어질 때 그 객체에 연결` 됩니다.

```js
function Ultra(){}
Ultra.prototype.ultraProp = true;
 
function Super(){}
Super.prototype = new Ultra();
 
function Sub(){}
Sub.prototype = new Super();
 
let o = new Sub();
console.log(o.ultraProp);   // true
```
> 3개의 생성자(Ultra, Super, Sub)가 있으며 Ultra라는 최상위 객체와 중간에 Super가 있고 맨 밑에 Sub가 있다고 보면 sub는 Super에 상속받고 Super는 Ulter를 상속받습니다.
즉 Sub에 정의 되지 않은 .ulterProp는 Ultra에서 상속받아와 `new` 생성자를 통해서 o라는 변수 안에는 생성자로 만들어진 Sub()객체가 전달되어 출력되게 됩니다.

## prototype chain
> 자바스크립트에서 속성이나 메서드를 참조하게 되면, 먼저 자신안에 정의되어있는지 찾아보고 없다면 그 프로토타입으로 이동해(상위) 해당 프로토타입 객체 내에 정의를 찾습니다. 이러한 객체들의 연쇄를 가리켜 `프로토타입 체인(Prototype Chain)`이라고 합니다.
- 예제
```js
function Ultra(){}
Ultra.prototype.ultraProp = true;
 
function Super(){}
Super.prototype = new Ultra();
 
function Sub(){}
Sub.prototype = new Super();
Sub.prototype.ultraProp = 2;
 
let o = new Sub();
//o.ultraProp = 1;

console.log(o.ultraProp);
```
> 변수 o는 생성자를 통해 Sub에 ultraProp가 있는지 찾게 되고 `Sub.prototype.ultraProp = 2`가 있기 때문에 값을 가져와 2라는 결과를 보여주게 됩니다.

- 추가 예제

```js
function Ultra(){}
Ultra.prototype.ultraProp = true;
 
function Super(){}
let t = new Ultra();
Super.prototype = t;
 
function Sub(){}
let s = new Super();
Sub.prototype = s;
 
let o = new Sub();

console.log(o.ultraProp);
```
> 생성자의 프로토타입을 찾아서 Sub.prototype = s;로 Super의 프로토타입에 t는 Ultra의 프로토타입을 찾아 .ultraProp를 찾아 결과를 true로 받아오게 됩니다.