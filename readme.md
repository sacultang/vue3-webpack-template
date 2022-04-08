# VUE3 WEBPACK TEMPLATE

```
$ npm i vue // 메이저 2버전 설치
$ npm i vue@next // 3버전 설치
```

vue확장자를 관리하려면 webpack 패키지를 설치 해야함
```
$ npm i -D vue-loader // 2버전 설치
$ npm i -D vue-loader@next // 3버전 설치
$ npm i -D vue-style-loader
$ npm i -D @vue/compiler-sfc // vue파일을 브라우저에서 변환해서 동작하는 패키지

```

## webpack.config.js

```js
webpack.config.js에 작성

const { VueLoaderPlugin } = require('vue-loader)
module.exports = {
  module: {
    rules: [
      {
        test:/\.vue$/,
        use:'vue-loader' //webpack이 vue확장자 파일을 해석
      },
      {
        test:/\.s?css$/,
        use: [
          'vue-style-loader', // 마지막에 읽어 드릴수 있도록 순서 중요
          'style-loader', // 순서 4.해석된 내용을 html에 삽입해주는 역할 
          'css-loader', // 순서 3.자바스크립트에서 css를 해석하기 위한 패키지
          'postcss-loader', //순서 2
          'sass-loader' // 순서 1. sass loader
        ]
      }
    ]
  },
  plugins : [
    new VueLoaderPlugin()
  ]
}
```

## 확장자 생략
```js
webpack.config.js에 작성

module.exports = {
  resolve: {
    extensions:['.js','.vue'] //js와 vue 확장자명 생략 가능
  },
}
```

## 경로 별칭
```
$ npm i -D file-loader
```
```js
webpack.config.js에 작성

const path = require('path') //따로 설치 하지 않고 node에서 사용가능한 전역 모듈
module.exports = {
  resolve :{
    alias :{ //경로별칭 해당하는 경로별칭이 지칭하는 곳으로 점프 뜀
      '~':path.resolve(__dirname,'지칭할 경로(src)'),
      'assets':path.resolve(__dirname,'src/assets')
    }
  },
  module : {
    rules:[
      {
        test:/\.(png|jpe?g|gif|webp)$/,
        use:'file-loader // 파일이 정상적으로 해석 됨
      }
    ]
    
  }
}
```
## ESLINT
```
$ npm i -D eslint
$ npm i -D eslint-plugin-vue
$ npm i -D babel-eslint
```
- vue eslint
https://eslint.vuejs.org/user-guide/
```js
.eslintrc.js 에 작성

module.exports = {
  env: {
    browser:true, // 코드를 브라우저와 노드에서 모두 검사 할건지 여부
    node: ture
  },
  extends : [  // 코드 검사를 할 기본적인 규칙 작성
  //vue
   // 'plugin:vue/vue3-essential', // Lv1
    'plugin:vue/vue3-strongly-recommended', // Lv2
    // 'plugin:vue/vue3-recommended', // Lv3 가장 엄격한 코드 검사
    //js
    'eslint:recommended'
  ],
  parserOptions : { // 코드를 분석할 수 있는 분석기를 지정
    parser : 'babel-eslint'
  },
  rules:{
    // 입맛에 맞는 규칙 설정
  }
}
```
