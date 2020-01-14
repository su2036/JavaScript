# 비교
cf)  
    null : 값이 없습니다.  
    undefined : 정의 되어 있지 않습니다.
    NaN : 0/0, 성립하지 않는 수, 계산할 수 없습니다.
```javascript
console.log(null == undefined);     // true
console.log(null === undefined);    // false
console.log(true == 1);             // true
console.log(true === 1);            // false
console.log(true == '1');           // true
console.log(true === '1');          // false
console.log(0 == -0);               // true
console.log(NaN === NaN);           // false
```
> 데이터 타입에 따라 다릅니다  
cf) [==과 ===의 차이점 참고 링크](https://dorey.github.io/JavaScript-Equality-Table/)

<hr />

## 부정과 부등호

### !==
> '!=='는 '!='와 '=='의 관계와 같습니다. 그리고 정확하게 같지 않다는 의미입니다.
- 예제  
```javascript
console.log(1!=2);            //true
console.log(1!=1);            //false
console.log("one"!="two");    //true
console.log("one"!="one");    //false
```
### >
> 좌항이 우항보다 크거나 같다라는 정의의 부등호입니다. `<=`는 반대의 의미입니다.
```javascript
console.log(10>=20);        //false
console.log(10>=1);         //true
console.log(10>=10);        //true
console.log(10<=20);        //tree
```
