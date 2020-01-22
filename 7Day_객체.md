# 객체

## Class를 통한 객체생성
- ES6 Class
    > javascript에는 class가 없습니다. 다만 class라는 키워드가 생겼습니다.
    인스턴스는 "new" 키워드 사용해서 만든다.

- 예제, 기존의 this context방법
```javascript
function Health(name){      // Health는 name이라는 단일 프로퍼티를 생성하는 생성자 함수
    this.name = name;
}

Health.prototype.showHealth = function() {  // Health함수 아래 prototype객체를 이용해 prototype안의 
                                            //showHealth메서드는 객체간의 재사용되는 것을 참조할 수 있음.
    console.log(this.name + "님 안녕하세요");
}

const h = new Health("Changsu");    // new 키워드를 사용해 객체를 생성
h.showHealth(); // "Changsu님 안녕하세요"
```

- 예제, ES6 class로 개편
```javascript
class Health {
    constructor(name, Time) {   // 생성자 함수와 동일
        this.name = name;
        this.Time = Time;
    }

    showHealth() {      // prototype에 저장되며 함수이다.(즉, Health.prototype.showHealth와 동일)
        console.log("안녕하세요 " + this.name + "님 지금 시간은 " + this.Time + "시 입니다.");
    }
}

const myHealth = new Health("Changsu", 12);
myHealth.showHealth();
```

- 결과  
![스크린샷 2020-01-22 오후 11 16 28](https://user-images.githubusercontent.com/29330085/72901617-70b71e00-3d6d-11ea-9e56-24b588b7f489.png)  

> class를 이용해서 가독성이 좋아졌습니다.


## Object assign으로 JS객체만들기
> class와 모듈을 만들때 유용합니다.

- 예제, es5 object create
```javascript
const healthObj = {
    showHealth : function() {
        console.log("오늘 운동시간 : " + this.healthTime);
    }
}

const myHealth = object.create(healthObj);  // prototype 오브젝트 생성
myHealth.healthTime = "11:20";
myHealth.name = "changsu";

console.log(myHealth);
```
- 결과  
![스크린샷 2020-01-22 오후 11 31 07](https://user-images.githubusercontent.com/29330085/72902709-4ebe9b00-3d6f-11ea-8e5a-839ba63141ea.png)
    > myHealth에 healthTime에 "11:20"과 name에 "changsu"가 있는걸 확인 할수 있고  
    myHealth가 `일반 오브젝트안에 포함된게 아닌 prototype의 객체`로 나오는 것을 확인 할 수 있습니다.   
    위에서 함수 만들고 그 생성자 안에 prototype.showHealth를 안해줘도 쉽게 객체를 만들 수 있습니다.  
    그러나, .healthTime .name처럼 일일히 다 저장해줘야하는 문제가 있습니다.

- 예제, ES6로 Object Assign 사용
```javascript
const healthObj = {
    showHealth : function() {
        console.log("오늘 운동시간 : " + this.healthTime);
    }
}

const myHealth = Object.assign(Object.create(healthObj),{   // Object.assign은 create값과 넣을 값(name, healthTime)을 같이 담아줘서 사용 가능
    name : "Changsu",
    healthTime : "11:30"
});

console.log("나의 운동시간은 ", myHealth);
myHealth.showHealth();
```
- 결과  
![스크린샷 2020-01-23 오전 12 11 44](https://user-images.githubusercontent.com/29330085/72906069-f5f20100-3d74-11ea-8aa7-833eca3de4b1.png)  


## Object assign으로 Immutable객체 만들기(새로운 객체 만들기)
> 객체 안에 있는 값을 변형시켜서 속성값을 뽑아서 다른걸로 만드는 것입니다 = COPY!!
- 예제, new 라는 값이 없이도 class형태로 만들 수 있다.
```javascript
const previousObj = {
    name : "changsu",
    lastTime : "11:30"
};

const myHealth = Object.assign({}, previousObj, {   
    "lastTime" : "1:30",
    "age" : 10
});

console.log(previousObj, myHealth);
```

- 결과  
![스크린샷 2020-01-23 오전 12 45 08](https://user-images.githubusercontent.com/29330085/72909000-aeba3f00-3d79-11ea-8c4b-4c069983c42a.png)
> Object.assign(`{}`, previousObj, {})여기에서 강조된 {}부분엔 프로토타입 오브젝트가 되게됩니다.  
Object.assign({}, `previousObj`, {})여기에서 강조된 perviousObj의 오브젝트 값을 다 추출 한다음 그중에 새로운 값이 뒤{}에 있다면 대체를 하고 없다면 그대로 출력하게 됩니다.  
그 결과 age와 lastTime의 값이 추가되고 변경 된것을 결과로 볼 수 있습니다.

- 추가 예제, 서로의 값은 같은가?
```javascript
const previousObj = {
    name : "changsu",
    lastTime : "11:30"
};

const myHealth = Object.assign({}, previousObj, {});    // 대체할 것이 없을때 그대로 출력
console.log(myHealth);      // name : changsu , lastTime : 11:30
console.log(previousObj);   // name : changsu , lastTime : 11:30
console.log(previousObj === myHealth);  // false
```
- 결과  
![스크린샷 2020-01-23 오전 12 52 40](https://user-images.githubusercontent.com/29330085/72909647-b3332780-3d7a-11ea-92f4-d09990199962.png)
> 위 코드의 결과를 보다 싶이 myHealth와 previousObj의 값은 같아도 서로 다른 값이라는 것을 알 수 있습니다. 즉, 저장에 또 다른 위치에 저장하는 것입니다.




## Object setPrototypeOf로 객체 만들기
> ~에 prototype으로 객체에 추가, 세팅한다는 의미입니다.

```javascript
const healthObj = {
    showHealth : function() {
        console.log("오늘 운동시간 : " + this.healthTime);
    },
    setHealth : function(newtime) {
        this.healthTime = newTime;
    }
}

const myHealth = {      // 일반 객체 생성
    name : "Changsu",
    lastTime : "11:30"
};

Object.setPrototypeOf(myHealth, healthObj); //myHealth 오브젝트에 healthObj를 추가

console.log("내 운동시간은 ", myHealth);
```
- 결과  
![스크린샷 2020-01-23 오전 1 08 31](https://user-images.githubusercontent.com/29330085/72911132-e676b600-3d7c-11ea-9620-a67db700dd33.png)
> 이렇게 일반 객체였던 myHealth에 프로토타입 객체가 추가 되게 됩니다.

- 예제, Object.create를 쓰지 않고 프로토타입 오브젝트 추가하기
```javascript
const healthObj = {
    showHealth : function() {
        console.log("오늘 운동시간 : " + this.healthTime);
    },
    setHealth : function(newtime) {
        this.healthTime = newTime;
    }
}

const newObj = Object.setPrototypeOf({  // 바로 오브젝트를 넣어서 사용 가능
    name : "Changsu",
    lastTime : "11:30"
}, healthObj);

console.log(newObj);
```
- 결과  
![스크린샷 2020-01-23 오전 1 25 53](https://user-images.githubusercontent.com/29330085/72912665-50905a80-3d7f-11ea-8b29-bb8ce4fe0c4e.png)
  

## Object setPrototypeOf로 객체간 prototype chain생성하기
> 객체 만든걸로 재사용해서 합칠수 있습니다. 상속을 이용할 수 있는 개념입니다.

```javascript
//perent
const healthObj = {
    showHealth : function(){
        console.log("오늘 운동시간 : " + this.healthTime);
    },
    setHealth : function(newTime){
        this.healthTime = newTime;
    }
}
//child obj
const healthChildObj = {
    getAge : function() {   // 메서드 생성
        return this.age;
    }
}

Object.setPrototypeOf(healthChildObj, healthObj); // const lastHealthObj선언문이 생략됨
                                                  // healthChildObj에 프로토타입 체인으로 healthObj가 들어간다.

const childObj = Object.setPrototypeOf({
    age : 22
}, healthChildObj);

childObj.setHealth("11:55");    // childObj에 setHealth가 없으므로 프로토타입 체인을 타고 올라가서 
childObj.showHealth();          // healthObj의 showHealth를 찾음
```
- 결과  
![스크린샷 2020-01-23 오전 2 09 36](https://user-images.githubusercontent.com/29330085/72916476-6d2f9100-3d85-11ea-8b4d-4ed6d4b3752d.png)


const healthObj = { 
    showHealth : function(){ 
        console.log("오늘 운동시간 : "+this.healthTime); 
    }, 
    setHealth : function(newTime){ 
        this.healthTime = newTime; 
    } 
} 
const healthChildObj ={ 
    getAge : function (){ return this.age; } } const lastHealthObj = Object.setPrototypeOf(healthChildObj,healthObj); 

const childObj = Object.setPrototypeOf({ age : 40, 
}, lastHealthObj);
console.log(childObj);
