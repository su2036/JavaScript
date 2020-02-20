# 객체지향 - THIS
> this는 함수 내에서 함수 호출 맥락(context)를 의미합니다.  맥락이라는 것은 상황에 따라서 달라진다는 의미인데 즉 함수를 어떻게 호출하느냐에 따라 this가 가리키는 대상이 달라진다는 뜻 입니다. 함수와 객체의 관계가 느슨한 JS에서 this는 이 둘을 연결시켜주는 실질적인 연결점의 역할 입니다.
## 함수와 this
### 함수호출
- 예제
```js
function func(){
    if(window === this){
        console.log("window === this");
    }
}
func();
```

- 결과  
![스크린샷 2020-02-20 오전 8 30 22](https://user-images.githubusercontent.com/29330085/74886357-459b0b00-53bb-11ea-92b0-dae4ec5f8ade.png)  
> 해당 함수에서 this라는 값이 전역객체를 의미하는 window를 의미합니다.


## 메소드와 this
메소드 안에서 this는 무엇인가.
### 메소드의 호출
```js
let o = {
    func : function(){  // 메소드
        if(o === this){ // o = 변수 o
            console.log("o === this");
        }
    }
}
o.func();
```
- 결과  
![스크린샷 2020-02-20 오전 8 33 10](https://user-images.githubusercontent.com/29330085/74886603-eab5e380-53bb-11ea-88be-a1b7574288eb.png)  

> 결과를 보면 o라는 변수에 객채로 메소드를 만들고 메소드를 호출하면 자기자신(o)를 호출 할 수 있다라는 의미입니다. 즉, 메소드를 호출할때 소속된 객체를 가르키게 됩니다.


## 생성자와 this
생성자 안에서 this는 무엇인가.

```js
let funcThis = null;

function Func(){        // 실행되면 상위에 funcThis를 가르킴
    funcThis = this;    // 생성자 this로 쓰일 땐, 객체 / 함수로 호출되게 되면 하위 window를 가르키게 됨
}
let o1 = Func();        // 실행시키면 상위에 funcThis = this가 실행됨
if(funcThis === window){
    document.write()
}

let o2 = new Func();    // 생성자를 호출하게 되면 생성자에 대한 호출이 모두 끝난 다음에 o2 변수에 객체가 할당됨
if(funcThis === o2){
    document.write('o2 <br />');
}
```
> 생성자 안에서 this는 그 생성자가 만든 객체를 가르킵니다.



## 객체로서 함수
> 함수의 메소드인 `apply, call`을 이용하면 this의 값을 제어할 수 있습니다.

```js
let o = {}  // 객체 리터럴, new Object
```
```js
let a = [1,2,3] // 배열리터럴, new Array(1,2,3)
```
> 함수가 객체입니다.?
```js 
function sum(x,y){return x+y;}      // sum은 객체로 함수 객체를 만들어 줌 => 함수리터럴(literal)
sum(1,2);

let sum2 = new Function('x','y', 'return x+y;');    // 생성자 함수 호출(new Function), return x+y; 인자
sum2(1,2);
```


## apply와 this
- 예제, 함수를 apply로 호출했을 때 내부적으로 this의 값은 어떻게 변경됬을까?
```js
let o = {}
let p = {}
function func(){
    switch(this){   // this->window, switch = if대체제 /ex) for = while대체제
        case o:
            document.write('o<br />');
            break;
        case p:
            document.write('p<br />');
            break;
        case window:
            document.write('window<br />');
            break;          
    }
}
func();         // this가 window가 됨
func.apply(o);  // 메소드인 apply호출 첫번째 인자로 this에 o가 됨
func.apply(p);
```
> 함수가 누구의 소속이냐에 따라 this의 값은 그 소속객체에 종속되며 값이 다릅니다.


