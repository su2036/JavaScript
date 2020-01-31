# 배열
> 배열(array)란 연관된(여러개) 데이터를 모아서 통으로 관리하기 위해서 사용하는 데이터 타입입니다.

## 배열의 문법
- 배열 생성
    ```javascript
        let member = ['a', 'b', 'c']

        document.wirte(member);  // a, b, c
    ```

- 예제  
```javascript
let member = ['a', 'b', 'c']    // 각각의 데이터는 원소라고 부름.

document.wirte(member[0]);   // 0
document.wirte(member[1]);   // 1
document.wirte(member[2]);   // 2
```

## 배열의 효용성
- 배열이 없다면
```javascript
function get_member1(){
    return 'a';     // return은 단 하나의 값만 반환함.
}
document.wirte(get_member1());

function get_member2(){
    return 'b';     // return은 단 하나의 값만 반환함.
}
document.wirte(get_member1());

function get_member3(){
    return 'c';     // return은 단 하나의 값만 반환함.
}
document.wirte(get_member1());

```

- 배열을 이용
```javascript
function get_member(){      // get_member는 a,b,c 값이 들어있음
    return ['a', 'b', 'c'];
}
let members = get_member(); // members는 get_member를 할당하며

document.wirte(members[0]);  // a
document.wirte(members[1]);  // b
document.wirte(members[2]);  // c
```

> 배열은 이렇게 여러가 원소, 값들을 하나로 모은 통이라 할수 있습니다. 또, 배열은 순차적이기 때문에 members[0]은 첫번째인 a,

## 배열의 사용 - 배열과 반복문
> 반복문으로 리스트에 담긴 정보를 하나씩 꺼내서 처리 할 수 있습니다.

```javascript
function get_member(){
    return['a', 'b', 'c'];
}

members = get_member();

document.wirte(members[0].toUpperCase());    // A, toUpperCase내장함수로 대문자로 변경해줌
```
> `members[0]`으로 0번째 a만 출력이 되게 되고 `toUpperCase()`라는 내장함수로 인해 소문자a가 아닌 대문자 A가 출력되게 됩니다.

- 반복문 사용하기
```javascript
function get_member(){
    return ['a', 'b', 'c'];
}

members = get_member();

for(let i = 0; i<3; i++){
    document.write(members[i].toUpperCase() + "<br />");
}
```
- 결과  
```
A
B
C
```
> `get_member()함수`를 `members`로 호출하고 반복문에서 배열이 3개가 있기 때문에 `i < 3`을 줘서 `members[i].toUpperCase()`를 통해 대문자 ABC를 확인할 수 있습니다.

- 배열의 개수와 상관 없이 모두 출력해보자

```javascript
function get_member(){
    return ['a', 'b', 'c', 'd'];
}

members = get_member();

for(let i = 0; i < members.length; i++){
    document.write(members[i].toUpperCase() + "<br />");
}
```
- 결과  
```
A
B
C
D
```
> 반복문에서 `i < 3`이아닌 `i < members.length`를 통해 리턴 받는 배열의 갯수가 3이아닌 4가 되도 모두 출력 하게 됩니다.

## 배열의 조작 - 추가

- 하나의 배열 추가!, PUSH
```javascript
let li = ['a', 'b', 'c', 'd', 'e'];

li.push('f');

alert(li);
```
> 결과  
![스크린샷 2020-01-31 오전 8 48 28](https://user-images.githubusercontent.com/29330085/73500693-ba0b0b80-4406-11ea-957b-d2a6bda853b8.png)


- 여러개의 배열 추가!, CONCAT
```javascript
let li = ['a', 'b', 'c', 'd', 'e'];

li = li.concat(['f', 'g']);   // concat함수를 이용해 하나의 배열을 추가로 li에 다시 리턴하게함. 

alert(li);
```
- 결과  
![스크린샷 2020-01-31 오전 8 53 14](https://user-images.githubusercontent.com/29330085/73500836-2554dd80-4407-11ea-81c4-47bbd0b2b989.png)  

- 배열 맨 앞에 추가!, unshift
```javascript
let li = ['a', 'b', 'c', 'd', 'e'];

li.unshift('z'); 

alert(li);
```
- 결과  
![스크린샷 2020-01-31 오전 8 55 58](https://user-images.githubusercontent.com/29330085/73500953-8977a180-4407-11ea-825b-a49fbc1b8882.png)  
> `li.unshift`로 인해서 z가 li 배열 맨 앞에 추가 된것을 확인 할 수 있습니다.

- 중간에 추가!, splice
  - 문법
  ```
  array.splice (index, howmany, element1, ..., elementN);
  ```
  > `index`는 배열에 추가할 특정 배열의 위치, 꼭써야함.  
  `howmany`는 index에서 부터 제거될 원소들의 수. index+howmany에 해당하는 원소들은 삭제된다.   
  이 값이 0이면 어떠한 원소도 삭제 되지 않는다.  
  `element`는 추가될 값.

```javascript
let li = ['a', 'b', 'c', 'd', 'e'];

li.splice(1, 1, 'z'); 

alert(li);
```
- 결과  
![스크린샷 2020-01-31 오전 9 13 37](https://user-images.githubusercontent.com/29330085/73501674-fab85400-4409-11ea-9b3d-ac104ef3aac2.png)  

> `li.splice(1, 1, 'z')`에서 index 1인 배열의 1번자리 'b'를 가르키고 그다음 howmany의 값이 1이기 떄문에 b를 삭제하고 'z'가 추가 된것을 확인 할 수 있습니다.

## 배열의 조작 - 제거, 정렬
- 제거, shift : 첫번째 원소를 제거하는 방법
```javascript
let li = ['a', 'b', 'c', 'd', 'e'];

li.shift();

alert(li);
```
- 결과  
![스크린샷 2020-01-31 오전 9 15 59](https://user-images.githubusercontent.com/29330085/73501789-51be2900-440a-11ea-995b-bcacd5269ee7.png)

- 제거, pop : 배열 끝점의 원소를 제거하는 방법
```javascript
let li = ['a', 'b', 'c', 'd', 'e'];

li.pop();

alert(li);
```
- 결과  
![스크린샷 2020-01-31 오전 9 17 33](https://user-images.githubusercontent.com/29330085/73501867-88943f00-440a-11ea-9779-0834207d3169.png)  

- 정렬, sort
```javascript
let li = ['c', 'b', 'd', 'a'];

li.sort();

li;
```
- 결과  
![스크린샷 2020-01-31 오전 9 21 06](https://user-images.githubusercontent.com/29330085/73502056-1a9c4780-440b-11ea-9cd5-13218fa10d81.png)

- 정렬, reverse : 역으로 정렬
```javascript
let li = ['c', 'b', 'd', 'a'];

li.reverse();

li;
```
- 결과  
![스크린샷 2020-01-31 오전 9 21 29](https://user-images.githubusercontent.com/29330085/73502060-1f60fb80-440b-11ea-9d7c-7df7b7a9a69b.png)
