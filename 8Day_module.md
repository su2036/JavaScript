# MODULE
## module(export & import)의 이해
- 실습
    - myLogger.js
    ```javascript
    export default function log(data) { // export로 생략 가능하며 객체로 넘긴다.
        console.log(data);
    }
    ```

    - app.js
    ```javascript
    import log from './myLogger'    // 객체로 넘어와 log라는 함수를 쓰겠다, ./myLogger.js이지만 웹팩에서 알아서 가져와준다!!

    const root = document.querySelector('#root');
    root.innerHTML = `<p>Hello World ! </p>`;
    log('my first test data');
    ```

> export default를 export로 생략해서 쓰면 import로 받을때 `import {log} from './myLogger'`로 사용하며, log라는 함수를 받아와 쓰게 됩니다.


## module(export & import)기반 서비스코드 구현 방법
- 시간 값을 반환하는 함수
    - myLogger.js
    ```javascript
    export default function log(data) { // export default로 기본으로 쓰겠다!
        console.log(data);
    }

    export const getTime = () => {
        return Date.now();
    }

    export const getCurrentHour = () => {
        return (new Date).getHours();
    }
    ```

    - app.js
    ```javascript
    import log, {getTime, getCurrentHour} from './myLogger'    // 객체로 넘어와 log, getTime, getCurrentHour라는 함수를 쓰겠다.

    log('my first test data');                      // my first test data
    log(`getTime is ${getTime()}`);                 // getTime is 1498012209935??
    log(`Current hour is ${getCurrentHour()}`);     // Current hour is 9
    ```

- Class를 사용해 개발하기
    - myLogger.js
    ```javascript
    export default function log(data) { // export default로 기본으로 쓰겠다!
        console.log(data);
    }

    export const getCurrentHour = () => {
        return (new Date).getHours();
    }

    /* Class */
    export class MyLogger {
        constructor(props) {
            this.lectures = ['java', 'ios'];
        }
        getLectures() {
            return this.lectures;
        }
        getTime() {
            return Data.now();
        }
    }
    ```

    - app.js
    ```javascript
    import log, {getCurrentHour, MyLogger} from './myLogger'    // 객체로 넘어와 log, getTime, getCurrentHour라는 함수를 쓰겠다.

    log('my first test data');                      // my first test data
    log(`Current hour is ${getCurrentHour()}`);     // Current hour is 9

    const logger = new MyLogger();                  // MyLogger는 Class, 생성자 함수이므로 new를 사용한다.
    log(`lectures of Codesquad are ${logger.getLectures()}`);   // lectures of Codesquad are java, ios

    ```

- 여러개 모듈 사용하기, utility export
    - utility.js
    ```javascript
    const _ = {      // export default와 const는 함께 쓰지 못함!!
        log(data) {
            if(windows.console) console.log(data);
        }
    } 
    export default _;
    ```

    - CodeSquad.js
    ```javascript
    export default class CodeSquad {
        constructor(props) {
            this.lectures = ['java', 'ios'];
        }
        getLectures() {
            return this.lectures;
        }
        getCurrentHour() {
            return (new Date).getHours();
        }
        getTime() {
            return Data.now();
        }
    }
    ```

    - app.js
    ```javascript
    import  CodeSquad from './CodeSquad';
    import _ from './utility';
    

    _.log('my first test data');                            // my first test data

    const cs = new CodeSquad();                             // MyLogger는 Class, 생성자 함수이므로 new를 사용한다.
    _.log(`Current hour is ${cs.getCurrentHour()}`);        // Current hour is 9
    _.log(`lectures of Codesquad are ${cs.getLectures()}`); // lectures of Codesquad are java, ios

    ```






