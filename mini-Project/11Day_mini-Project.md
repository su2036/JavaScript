## XHR통신
> 블로그 리스트를 받아서 html을 구성하기
- XMLHttpRequest 프로그래밍 순서  
    1. XMLHttpRequest 객체 구하기
        - IE : ActiveX컴퍼넌트로 제공
        - 다른 브라우저 : XMLHttpRequest클래스를 기본적으로 제공
    2. 웹 서버에 요청 전송하기
    3. 웹 서버에서 응답이 도착하면 화면에 반영하기

```html
<section class="blogList">
		<ul></ul>
```
> 안에 추가 하도록 하겠습니다.  
추가 하기전 `<ul>`태그 안에 넣을 데이터를 가져옵니다. 

- main.js
```javascript
class Blog{
	constructor(){
	console.log('Blog is stated!!!!!~~~');
	const dataURL = "http://dummy.restapiexample.com/api/v1/employees";
	this.setInitData(dataURL);
	}
	
	setInitData(dataURL) {
		this.getData(dataURL);
		//do someting...
	}

	getData(dataURL) {	// 필요한 url에 데이터를 가져옴, AJAX호출
		const oReq = new XMLHttpRequest();			// 생성자함수, 즉 생성하고 초기화

		oReq.addEventListener("load", () => {						// 로딩이 완료되면 
			const list = JSON.parse(oReq.responseText).data;		// data를 받아온다

			list.forEach((v) => {					// 반복
				console.log(v.employee_name);
			})
		});

		oReq.open('GET', dataURL);		// get방식으로 dataURL을 받아와 Ajax 요청
		oReq.send();					// 작성된 Ajax 요청을 서버로 전달
	}

}

export default Blog;
```


## bloglist 추가
- innerhtml사용하기

```javascript
class Blog{
	constructor(){
	console.log('Blog is stated!!!!!~~~');
	const dataURL = "http://dummy.restapiexample.com/api/v1/employees";
	this.setInitData(dataURL);
	}
	
	setInitData(dataURL) {
		this.getData(dataURL, this.insertPosts);    // callback->list.forEach을 넘기기위해 메서드 생성
		//do someting...
	}

	getData(dataURL, fn) {	// 필요한 url에 데이터를 가져옴, 콜백 함수를 받아옴
		const oReq = new XMLHttpRequest();			// 생성자함수, 즉 생성하고 초기화

		oReq.addEventListener("load", () => {						// 로딩이 완료되면 
			const list = JSON.parse(oReq.responseText).data;		// data를 받아온다
            fn(list);
		});
		oReq.open('GET', dataURL);		// get방식으로 dataURL을 받아와 Ajax 요청
		oReq.send();					// 작성된 Ajax 요청을 서버로 전달
	}

    insertPosts(list) {
        
        const ul = document.querySelector(".blogList > ul");

        list.forEach((v) => {
            ul.innerHTML +=`<li>${v.employee_name} </a></li>`	// 블로그 주소(link)와 데이터 입력
        })
    }
}

export default Blog;
```
- 결과  
![스크린샷 2020-02-03 오전 1 26 54](https://user-images.githubusercontent.com/29330085/73611358-6bd35380-4624-11ea-921e-06239770853b.png)


## set자료에 데이터 추가(찜하기기능)

```javascript
class Blog{
	constructor(){
		this.setInitVariables();
		this.registerEvents();
		this.likedSet = new Set();
	}

	setInitVariables() {
		this.blogList = document.querySelector(".blogList > ul");

	}

	registerEvents() {
		const startBtn = document.querySelector(".start");
		const dataURL = "http://dummy.restapiexample.com/api/v1/employees";
	
		startBtn.addEventListener("click", () => {
			this.setInitData(dataURL);
		});

		this.blogList.addEventListener("click", ({target}) => {
			const targetClassName = target.className;
			//classname이 like라면 내 찜하기목록에 새로운 블로그 제목을 추가한다.
			if(targetClassName !== "like") return;
			const postemployee_name = target.previousElementSibling.textContent;
			this.likedSet.add(postemployee_name);

			this.likedSet.forEach( (v) => {
				console.log('set data is', v);
			})
		});
	}
		
	setInitData(dataURL) {
		this.getData(dataURL, this.insertPosts.bind(this));    // bind를 시킴으로써 하단에 list에서도 사용 가능하게 함.
	}

	getData(dataURL, fn) {	// 필요한 url에 데이터를 가져옴, 콜백 함수를 받아옴
		const oReq = new XMLHttpRequest();			// 생성자함수, 즉 생성하고 초기화

		oReq.addEventListener("load", () => {						// 로딩이 완료되면 
			const list = JSON.parse(oReq.responseText).data;		// data를 받아온다
            fn(list);
		});
		oReq.open('GET', dataURL);		// get방식으로 dataURL을 받아와 Ajax 요청
		oReq.send();					// 작성된 Ajax 요청을 서버로 전달
	}

    insertPosts(list) {
    	list.forEach((v) => {
    		this.blogList.innerHTML +=`
    		<li>
    			<a>${v.employee_name}</a>
            	<div class="like">찜하기</div> 
            </li>
            `;	// 블로그 주소(link)와 데이터 입력
        })
    }
}

export default Blog;
```
- 결과  
![스크린샷 2020-02-03 오전 4 01 40](https://user-images.githubusercontent.com/29330085/73613520-e8246180-4639-11ea-9a54-0449c806101d.png)


## 찜목록뷰 업데이트


```javascript
class Blog{
	constructor(){
		this.setInitVariables();
		this.registerEvents();
		this.likedSet = new Set();
	}
	setInitVariables() {
		this.blogList = document.querySelector(".blogList > ul");
	}

	registerEvents() {
		const startBtn = document.querySelector(".start");
		const dataURL = "http://dummy.restapiexample.com/api/v1/employees";	
	
		startBtn.addEventListener("click", () => {
			this.setInitData(dataURL);
		});

		this.blogList.addEventListener("click", ({target}) => {
			const targetClassName = target.className;
			if(targetClassName !== "like" && targetClassName !=="unlike")return;
			
			const postemployee_name = target.previousElementSibling.textContent;

			if(targetClassName === "unlike") {
				target.className = "like";
				target.innerText = "찜하기";
				this.likedSet.delete(postemployee_name);
			} else {
				target.className = "unlike";
				target.innerText = "찜취소";
				this.likedSet.add(postemployee_name);
			}
			// 내 찜 목록 뷰에 추가.
			this.updateLikedList();
		
		});
	}

	updateLikedList() {
		const ul = document.querySelector(".like-list > ul");
		let likedSum = "";

		// li태그에 찜리스트를 넣고 한번의 innerHTML을 사용.
		this.likedSet.forEach ((v) => {
			likedSum += `<li> ${v} </li>`;
		})
		
		ul.innerHTML = likedSum;
	}
		
	setInitData(dataURL) {
		this.getData(dataURL, this.insertPosts.bind(this));    // callback->list.forEach을 넘기기위해 메서드 생성
	}

	getData(dataURL, fn) {	// 필요한 url에 데이터를 가져옴, 콜백 함수를 받아옴
		const oReq = new XMLHttpRequest();			// 생성자함수, 즉 생성하고 초기화

		oReq.addEventListener("load", () => {						// 로딩이 완료되면 
			const list = JSON.parse(oReq.responseText).data;		// data를 받아온다
            fn(list);
		});
		oReq.open('GET', dataURL);		// get방식으로 dataURL을 받아와 Ajax 요청
		oReq.send();					// 작성된 Ajax 요청을 서버로 전달
	}

    insertPosts(list) {
    	list.forEach((v) => {
    		this.blogList.innerHTML +=`
    		<li>
            	${v.employee_name}
            	<div class="like">찜하기</div> 
            </li>
            `;	// 블로그 주소(link)와 데이터 입력
        })
    }
}

export default Blog;
```
