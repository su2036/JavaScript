## nodeJS 기반 환경구성과 webpack
> MAC OS X 기준으로 기술하겠습니다.

- package.json 만들기  
`$ npm init`

- 웹팩 설치  
`$ npm install --save-dev webpack webpack-cli`
> `--save-dev`명령을 통해 package.json에 등록.  dev, 개발할떄만 쓰고 일반 다운받으면 안받아진데!!!

> `ls`명령을 통해 `node_modules`가 설치된것을 확인 할수 있습니다.

- ./webpack.config.js
```javascript
var path = require('path');

module.exports = {
        entry : './src/index.js',
        output : {
                filename : 'bundle.js',
                path:path.resolve(__dirname, 'dist')
        },
        module : {
                rules : [{
                }]
        }
}
```

- ./index.html
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta name="description" content="">
        <meta name="viewport" contecnt="width=device-width,initial-scale=1">
        <title>mini-Project</title>
    </head>
    <body>
        <h1>Hello N@D4</h1>
        <script src="./dist/bundle.js"></script>    <!--번틀 파일 가져오기-->
    </body>
</html>
```
- ./src/index.js
```javascript
console.log("start project by webpack");
```

- ./package.json
```json
{
  "name": "es6-inflearn",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "MODE_ENV=development webpack-dev-server --open",  "_comment_name_":"webpack 실행, 웹서버 열기",
    "build": "MODE_ENV=product webpack -p"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@babel/core": "^7.8.4",
    "@babel/preset-env": "^7.8.4",
    "babel-loader": "^8.0.6",
    "babel-preset-env": "^1.7.0",
    "babel-preset-es2015": "^6.24.1",
    "webpack": "^4.41.5",
    "webpack-cli": "^3.3.10",
    "webpack-dev-server": "^3.10.1"
  }
}
```
>package.json에서 `"start": "webpack"`를 추가.

- npm 실행  
`$ npm run start`

> /dist/bandle.js 파일이 생성된걸 확인가능

- 결과, 웹페이지 실행  
![스크린샷 2020-01-31 오전 12 51 42](https://user-images.githubusercontent.com/29330085/73465596-efdad080-43c3-11ea-9564-ea2eae0d1bc6.png)


## babel preset설정
- 왜 babel이 필요한가??  
> [ES2015지원 상황](http://kangax.github.io/compat-table/es6)  
ES6 => ES5 코드 변환필요!  
브라우저 상황은 계속해서 변한다!
최근 브라우저에 맞게 지원!

- babel7 설치  
`$ npm install --save-dev @babel/core babel-loader @babel/preset-env`

- babel7 설치 후 최근 2버전 브라우저 대응

```javascript
const webpack = require('webpack');
const path = require('path');

module.exports = {
    entry: './src/index.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        publicPath: '/dist/',
        filename: 'bundle.js'
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                include : path.resolve(__dirname, 'src'),
                exclude: /(node_modules)|(dist)/,
                use: {
                    loader: 'babel-loader',
                    options : {
                    	presets : [
                    		['@babel/preset-env',{
                    			'targets': {
                    				'browsers': ["last 2 versions"]
                    			},
                    			'debug': true   // 디버거로 대응하는 브라우저 정보와 버전 콘솔에서 확인
                    		}]
                    	]
                    }
                }
            }
        ]
    }
};
```
- 결과  
![스크린샷 2020-01-31 오전 2 30 31](https://user-images.githubusercontent.com/29330085/73474339-b27d3f80-43d1-11ea-9e35-2a77699c5aab.png)
> 이렇게 바벨에 디버거를 활용해 브라우저 정보와 버전을 콘솔에서 확인가능.

## webpack-dev-server와 html구성
> 일일이 코드를 수정하고 확인하기 위해 브라우저를 띄울 필요없이 코드 수정 후 바로 새로고침 해주게 구성하기

- package.json
```json
    "start": "MODE_ENV=development webpack-dev-server --inline --open"
```  

![스크린샷 2020-01-31 오전 2 38 17](https://user-images.githubusercontent.com/29330085/73474950-c1182680-43d2-11ea-9b1d-c8e35730db46.png)  

>위 코드로 기존엔 `--open`을 이용해 콘솔에서 `$ npm run start`를 하게되면 웹브라우저가 뜨게됩니다.   
여기서 바로바로 새로고침이 가능하도록 `--inline`을 추가해주면 됩니다.  
콘솔에 나와있듯이 dev server로 url주소에 port가 있는 것을 확인 할 수 있습니다.

