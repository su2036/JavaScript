# TEMPLATE
## Template처리
> 템플릿처리 json으로 응답을 받고, javascript object로 변환한 후에 어떠한 데이터처리 조작을 한 후에 dom에 추가.  
데이터 + HTML문자열의 결합이 필요하기 때문 중요합니다.

- 예제
  - JSON
  ```json
  const data = [
      {//0
        name : 'coffee-bean',
        order : true,
        items : ['americano', 'milk', 'green-tea']
      },
      {//1
          name: 'starbucks',
          order : false,
      }
  ]
  ```
  - JAVASCRIPT
  ```javascript
  const template = `<div>welcom ${data[0].name} !!`
  console.log(template);
  ```
  > ``(특수문자)를 사용하여 안에 있는 welcom 문자열에 `${data[0].name}`이라는 value값을 출력할 수 있습니다.  
  data[0]의 name키에 해당하는 값을 출력 할 것입니다.

  - 결과  
  ![스크린샷 2020-01-15 오전 6 53 32](https://user-images.githubusercontent.com/29330085/72385922-cedb7400-3763-11ea-9c2e-a79054906020.png)




## Tagged Template literals
> 여러줄로 이루어진 문자열의 표현과 문자의 치환을 쉽게 할 수 있는 기능이 있습니다.

- 예제
  - JSON
  ```json
  const data = [
      {//0
        name : 'coffee-bean',
        order : true,
        items : ['americano', 'milk', 'green-tea']
      },
      {//1
          name: 'starbucks',
          order : false,
      }
  ]
  ```
  - JAVASCRIPT
  ```javascript
    const template = `<div>welcome ${data[1].name} !!</div>
    <h2>주문가능항목</h2><div>${data[1].itmes}</div>`;
  ```
  >현재 위 코드는 출력이 불가능합니다. `${data[1].itmes}`의 itmes가 없기 때문입니다.  
  이대로 출력 결과를 보면
  - 결과 
  ![스크린샷 2020-01-15 오전 7 23 32](https://user-images.githubusercontent.com/29330085/72387888-f3d1e600-3767-11ea-8f0d-2d0b21ad61b0.png)  
  >itmes에 대한 값이 undefined로 출력 되는 것을 확인 할 수 있습니다.  
  해결 방법은 `function에서 처리를 한다음 결과값을 반환`하면 됩니다.

- 예제
  - JAVASCRIPT
    ```javascript
    function fnc(tags, name, items){
        console.log(tags);
    }

    const template = fnc`<div>welcome ${data[1].name} !!</div>
    <h2>주문가능항목</h2><div>${data[1].items}</div>`;
    ```  
    > 기존 html코드 내용을 `fnc로 function`으로 묶습니다.  
    위에서 function으로   
    tags = 배열로 `"<div>welcome"과 "</div><h2>주문가능항목</h2>" 그리고 "</div>"`,  
    name = `$data[1].name`,  
    items = `$data[1].items`  
    구분 할 수 있습니다.  

    - tags 결과  
    ![스크린샷 2020-01-15 오전 7 50 26](https://user-images.githubusercontent.com/29330085/72389445-b7a08480-376b-11ea-81dd-ec346b63c647.png)
    

    - name 결과  
    ![스크린샷 2020-01-15 오전 7 51 03](https://user-images.githubusercontent.com/29330085/72389483-cb4beb00-376b-11ea-85cd-877083785222.png)  

    - items 결과  
    ![스크린샷 2020-01-15 오전 7 52 00](https://user-images.githubusercontent.com/29330085/72389535-ee769a80-376b-11ea-9034-47823a17b5b2.png)  

- 예제, tagged templates으로 items에 "undefined" 해결하기
    ```javascript
    function fnc(tags, name, items){
        //console.log(items);
    if(typeof items === "undefined"){
        items = "주문가능한 상품이 없습니다요";
        }
        return (tags[0] + name + tags[1] + items + tags[2]);
    }

    const template = fnc`<div>welcome ${data[1].name} !!</div>
    <h2>주문가능항목</h2><div>${data[1].items}</div>`;

    console.log(template);
    ```  

    - 결과  
    ![스크린샷 2020-01-15 오전 8 34 53](https://user-images.githubusercontent.com/29330085/72391893-ede10280-3771-11ea-9516-5600878b7762.png)  

- 예제, forEach를 사용한 tagged tamplate literals 
```javascript
const data = [
    {
    name : 'coffee-bean',
    order : true,
    items : ['americano', 'milk', 'green-tea']
    },
    {
        name: 'starbucks',
        order : false,
    },
    {
    name : 'ediya',
    order : true,
    items : ['latte', 'milk-tea']
    }
]
function fnc(tags, name, items){
    //console.log(items);
  if(typeof items === "undefined"){
    items = "주문가능한 상품이 없습니다요";
  }
  return (tags[0] + name + tags[1] + items + tags[2]);
}

data.forEach((v) => { //화살표 함수
             
let template = fnc`<div>welcome ${v.name} !!</div>
  <h2>주문가능항목</h2><div>${v.items}</div>`;
  console.log(template);
});
```  
> forEach함수를 이용해 JSON 내용 data를 v로 대치하여 `화살표함수`를 사용해 모든 커피가게명과 주문 가능한 항목 및 불가 항목을 출력 할 수 있습니다.
- 결과  
![스크린샷 2020-01-15 오전 8 33 01](https://user-images.githubusercontent.com/29330085/72391821-a8bcd080-3771-11ea-82cf-609d54835d56.png)

cf) [화살표 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/애로우_펑션)
- 기본구문
``` 
    (param1, param2, …, paramN) => { statements }
    (param1, param2, …, paramN) => expression
    // 다음과 동일함:  => { return expression; }

    // 매개변수가 하나뿐인 경우 괄호는 선택사항:
    (singleParam) => { statements }
    singleParam => { statements }

    // 매개변수가 없는 함수는 괄호가 필요:
    () => { statements }
```