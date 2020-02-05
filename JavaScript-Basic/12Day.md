# 정규표현식
> 정규표현식(regular expression)은 문자열에서 특정한 문자를 찾아내는 도구입니다.  

 - [정규표현식 수업](https://opentutorials.org/course/909/5142)
 - ### 정규표현식 생성
    > 정규표현식은 두가지 단계로 이루어집니다. 하나는 `컴파일(compile)`다른 하나는 `실행(execution)`입니다.

## 패턴 만들기
- ### 컴파일(Compile)
> 컴파일은 검출하고자 하는 패턴을 만드는 일입니다.
- 정규표현식 리터럴
```js
let pattern = /a/;      // '/'와 '/'사이에 a를 찾고자한다!
```
- 정규표현식 객체 생성자
```js
let pattern = new RegExp('a');  // 정규표현식 객체를 만들어서 찾고자하는 패턴이 a다 라는 것.
```

## RegExp객체의 사용
- ### 정규표현식 메소드 실행
> 정규표현식을 컴파일해서 객체를 만들었다면 이제 문자열에서 원하는 문자를 찾아야합니다.

- RegExp.`exec`() : 추출
```js
console.log(pattern.exec('abcdef'));    //["a"]
```
- 결과  
![스크린샷 2020-02-06 오전 12 06 21](https://user-images.githubusercontent.com/29330085/73853707-aa5f4d00-4874-11ea-9035-17ac301a2406.png)  

    > 찾고자 하는 문자열은 'a'이며, 찾고자 하는 정보를 담고있는 'abcdef'(첫번쨰 인자)안에 'a'(두번째 인자)가 있는지 찾습니다.

- 예제 `'.'`
```js
let pattern = /a./;
console.log(pattern.exec('abcdef'));    // ["ab"]
```
- 결과  
![스크린샷 2020-02-06 오전 12 11 13](https://user-images.githubusercontent.com/29330085/73854263-923bfd80-4875-11ea-98f2-45271ad3c60b.png)
    > 찾고자 하는 문자열 `a`다음 `'.'`의 역활은 다음 하나의 문자를 더 찾는겁니다. 그리하여 'a'다음 'b'를 찾아 ["ab"]가 됩니다.

- 예제 찾고자 하는게 없을때.
```js
let pattern = /a/;
console.log(pattern.exec('bcdef'));     // null
```
- 결과  
![스크린샷 2020-02-06 오전 12 15 54](https://user-images.githubusercontent.com/29330085/73854451-ed6df000-4875-11ea-9b88-cee25a7ec01e.png)
    > 찾고자 하는 `a`가 없기 떄문에 배열로 찾아낼 값이 없어 `null`을 반환해줍니다.

- RegExp.`test`() : 존재 유무를 test, 결과를 `boolean`으로 반환해줍니다.
```js
let pattern = /a/;
console.log(pattern.test('abcdef'));    // true
console.log(pattern.test('bcdef'));    // false
```
- 결과  
![스크린샷 2020-02-06 오전 12 19 16](https://user-images.githubusercontent.com/29330085/73854748-535a7780-4876-11ea-97da-934679f05e9c.png)
    > test는 결과를 `boolean`으로 `true`와 `false`로 반환해주며, 찾고자 하는 'a'가 있는 'abcdef'는 `true`, 없는 'bcdef'는 `false`라는 결과를 확인 할 수 있습니다.


## String
- ### 문자열 메소드 실행
> 문자열 객체의 몇몇 메소드는 정규표현식을 사용할 수 있습니다.  

-`string.match`(), RegExp.exec()와 비슷합니다.
```js
let pattern = /a/;

console.log('abcdef'.match(pattern));   // ["a"]
console.log('bcdefg'.match(pattern));   // neull
```
- 결과  
![스크린샷 2020-02-06 오전 12 26 33](https://user-images.githubusercontent.com/29330085/73855473-76d1f200-4877-11ea-9d36-74ccdfad7d9a.png)![스크린샷 2020-02-06 오전 12 28 10](https://user-images.githubusercontent.com/29330085/73855560-9406c080-4877-11ea-8222-c89f591c520f.png)

-`string.replace`(), 문자열에서 패턴을 검색해서 이를 변경한 후에 변경된 값을 리턴합니다.
```js
let pattern = /a/;

console.log('abcdef'.replace(pattern, 'A'));    // Abcdef
```
- 결과  
![스크린샷 2020-02-06 오전 12 31 59](https://user-images.githubusercontent.com/29330085/73855934-198a7080-4878-11ea-9997-6eadc52930d8.png)  
    > 첫번째 인자로 `pattern`을 주고 두번째 인자로 바꾸고자 하는 문자`A`를 쓰면 해당되는 문자열 'abcdef'의 `a`가 `A`가 되는 것을 볼 수 있습니다.




