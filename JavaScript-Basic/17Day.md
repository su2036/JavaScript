# 함수지향 - 클로저
> 클로저(closure)는 내부함수가 외부함수의 맥락(context)에 접근할 수 있는 것을 가르킵니다.
## 내부함수, 외부함수
### 내부함수
> 자바스크립트는 함수 안에서 또 다른 함수를 선언할 수 있습니다.

- 예제, 함수안에 또 다른 함수를 선언
```js
function outter(){          // 외부함수
    function inner(){       // 내부함수
        let title = 'coding everybody';
        alert(title);
    }
    inner();
}
outter();
```
> `function inner()`는 `let inner=function(){}`와 같습니다. 결과는 경고창에 'coding everybody'가 출력 됩니다. `함수outter의 내부`에는 `함수inner가 정의` 되어 있습니다. 

- 예제, 내부함수는 외부함수의 지역변수에 접근 가능
```js
function outter(){          // 외부함수
    let title = 'coding everybody'; // 외부함수에 정의 되어있는 지역변수
    function inner(){       // 내부함수
        alert(title);
    }
    inner();
}
outter();
```
> inner 함수는 내부에 있는 `title`이라는 변수를 사용하려 했을때 inner라는 내부함수에 title이라는 정의된 지역변수가 존재하지 않는다면 `inner를 포함하는 함수 바깥쪽에 있는 함수(외부함수 outter)`에서 title이라는 변수를 찾게 됩니다.
즉, `바깥쪽에 title이라는 외부 함수에 있는 지역변수에 접근`할 수 있습니다.  
이러한 것을 `클로저(closure)`라고 합니다. 


## 클로저란?
> 클로저는 내부함수와 밀접한 관계를 가지고 있는 주제입니다. `내부함수는 외부함수의 지역변수에 접근` 할 수 있는데 외부함수의 실행이 끝나서 `외부함수가 사라진 이후에도 내부함수가 외부함수의 변수에 접근` 할 수 있습니다. 이 경우에도 클로저라고 합니다.

```js
function outter(){
    let title = 'coding everybody';
    return function(){
        alert(title);
    }
}
let inner = outter();
inner();    // inner라는 변수에 담겨있는 함수를 실행
```
> `외부함수(outter)는 종료`되었는데 외부함수로 인해 파생된 `내부함수에서 이미 종료되어 사라진 외부함수에 접근`해서 외부함수의 `지역변수인 title을 가져와 실행`하게 됩니다.


## private variable
> 비밀 변수...?, 아무나 실행하는 것을 방지하기 위함입니다.

```js
function factory_movie(title){      // 내부함수를 생성하고 있는 외부 함수의 지역변수에 접근 할 수 있음, 여기서 title은 프라이빗 변수임
    return {                        // 객체 안에 함수가 정의되어있음
        get_title : function(){     // get_title 메소드가 됨, 그리고 내부함수
            return title;           // 해당 title이라는 값은 factory_movie라는 함수의 첫번째 인자, 첫번째 매게변수는 title
        },
        set_title : function(_title){   // set_title 메소드가 됨, 그리고 내부함수
            title = _title          // _title은 title임, 그리고 title은 factory_movie의 title을 가짐
        }
    }
}
ghost = factory_movie('Ghost in the shell');    // 첫번째 호출
matrix = factory_movie('Matrix');               // 두번쨰 호출
alert(ghost.get_title());       // 경고창에 'Ghost in the shell'출력
alert(matrix.get_title());      // 경고창에 'Matrix'출력
ghost.set_title('공각기동대');     // 기존 'Ghost in the shell'에서 '공각기동대'로 설정

alert(ghost.get_title());       // 설정된 '공각기동대'로 출력
alert(matrix.get_title());      // 그대로 'Matrix'를 출력
```



## 클로저의 응용
```js
let arr = []
for(let i = 0; i < 5; i++){ // 5번 반복하면서 배열의 i 원소를 만듬
    arr[i] = function(id){  // 외부함수 id에 접근할수 있고 외부함수가 i값을 가짐
        return function(){
            return id;      // 내부함수가 id를 가지고
        }
    }(i);
}
for(let index in arr){      // for in 문을 이용해 배열에 값 하나하나를 index로
    console.log(arr[index]());  // 배열값 하나하나를 꺼내 결과를 볼 수 있음
}
```
- 결과  
![스크린샷 2020-02-13 오후 11 12 48](https://user-images.githubusercontent.com/29330085/74443386-698bb780-4eb6-11ea-9351-48093d008cba.png)  

> 클로저의 과정으로 내부 `return id;`의 id가 외부함수인 function(id)에 접근할 수 있고 그 외부함수 id는 for문의 i 값을 가지기 떄문에 결과는 0,1,2,3,4를 확인할 수 있습니다.


