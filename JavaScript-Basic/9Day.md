# 객체
- 객체(Object)
> 인덱스를 이용해서 데이터를 가져오게 되는데 즉, 데이터를 담아 내는 컨테이너입니다.  

## 객체의 생성
- 구조
```javascript
let grades = {'changsu' : 10, 'egoing' : 6, 'sorialgi' : 80};
```
> 객체에서 인덱스는 `문자(changsu, egoing, sorialgi)`이고 10, 6, 80 은 인덱스의 값입니다.  
객체를 `변수'grades'`에 담아 내면 변수를 통해 이 객체를 제어할 수 있게 됩니다.

- grades의 결과 보기  
![스크린샷 2020-02-02 오후 8 41 07](https://user-images.githubusercontent.com/29330085/73607672-69f59a00-45fc-11ea-8f79-46538b072c76.png)  

- 객체를 만드는 다른 방법 - 빈 객체
```javascript
let grades = {};            // 빈객체 생성가능.
grades['changsu'] = 10;     // []사이에 인덱스 값을 부여하고 인덱스의 값을 부여할 수 있음. 
grades['egoing'] = 10;
grades['sorialgi'] = 80;
```
> 여기서 `{}` 대신 `new Object()`로 사용할 수 있습니다.

- 예제, 객체를 만든 후 필요한 값을 가져오자!
```javascript
let grades = {'changsu' : 10, 'egoing' : 6, 'sorialgi' : 80};

alert(grades['changsu']);
alert(grades.changsu);
```
- 결과  
![스크린샷 2020-02-02 오후 8 53 50](https://user-images.githubusercontent.com/29330085/73607795-23a13a80-45fe-11ea-997e-3df57ee09250.png)  
    > 객체에서 `key,changsu`의 값 `value,10`을 가져올 수 있습니다.  
    또, `grades['changsu']`는 `grades['chan'+'su']`와 `grades.changsu`로 쓸 수 있으며 `grades.'chang'+'su'`로는 쓸 수 없습니다.
- 사용 결과  
![스크린샷 2020-02-02 오후 8 58 07](https://user-images.githubusercontent.com/29330085/73607838-bcd05100-45fe-11ea-8b09-26ab218927a2.png)  


## 객체와 반복문
cf) 배역은 순서가 있지만, 객체는 순서가 없지만 key와 value가 있습니다.

. 배열에 있는 값을 가져올땐 `for in문`을 사용합니다.
- 예제
```javascript
let grades = {'changsu' : 10, 'egoing' : 6, 'sorialgi' : 80};
for(let key in grades){
    console.log(key);           // 각 key값을 가져옴
    console.log(grades[key]);   // 각 key의 값을 가져옴
}
```

- 결과  
![스크린샷 2020-02-02 오후 9 19 00](https://user-images.githubusercontent.com/29330085/73608084-a5469780-4601-11ea-9cc7-b065f778f5fa.png)  

    > grades변수 안에 있는 객체 값들을 하나씩 가져와서 key값을 담아서 가져옵니다.   

- JavaScript로 HTML작성하기
```html
<html>
<head></head>
<body>
    <script>
        let grades = {'changsu' : 10, 'egoing' : 6, 'sorialgi' : 80};
        for(let name in grades){
            document.write("<li>key : " + name + " ,value : " + grades[name] + "</li>");
        }
    </script>
</body>
</html>
```
- 결과  
![스크린샷 2020-02-02 오후 9 27 52](https://user-images.githubusercontent.com/29330085/73608174-e55a4a00-4602-11ea-8066-8f2bb5837808.png)  



## 객체 지향 프로그래밍
> 객체에는 객체도 담을 수 있고 함수도 담을 수 있습니다.

- 객체 안에 객체 쓰기
```javascript
let grades = {
    'list' : {'changsu' : 10, 'egoing' : 8, 'sorialgi' : 80}
}

grades['list'];              // list 객체를 가르킴
grades['list']['changsu'];   // changsu키의 값을 가르킴
```
- 결과  
![스크린샷 2020-02-02 오후 10 14 45](https://user-images.githubusercontent.com/29330085/73608709-85b36d00-4609-11ea-95aa-abb392239895.png)


- 객체 안에 함수쓰기
```javascript
let grades = {
    'show' : function(){
        alert('hello world');
    }
}

grades['show']();            // show 함수 값 호출!
```
> 함수 값을 쓸땐 `grades['show']()`로 객체뒤 `()`를 붙여야 합니다.
- 결과  
![스크린샷 2020-02-02 오후 10 16 56](https://user-images.githubusercontent.com/29330085/73608729-bd221980-4609-11ea-8ddc-2a6238659688.png)
![스크린샷 2020-02-02 오후 10 17 20](https://user-images.githubusercontent.com/29330085/73608735-cc08cc00-4609-11ea-9548-513fa88a90eb.png)

- THIS 사용하기
```javascript
let grades = {
    'list' : {'changsu' : 10, 'egoing' : 8, 'sorialgi' : 80},
    'show' : function(){
        console.log(this.list);   // this.list는 'list'를 가르킴
    }
}

grades['show']();            // show 함수 호출!
```

- 결과  
![스크린샷 2020-02-02 오후 10 25 28](https://user-images.githubusercontent.com/29330085/73608825-eee7b000-460a-11ea-8a47-6a5d3e17a9e9.png)

