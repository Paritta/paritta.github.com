---
layout: post
title:  "[Webpack탐방기]Autohring Library"
author: "Paritta"
published: false
---

# [Webpack탐방기]Autohring Library 
참고: https://webpack.js.org/guides/author-libraries/

> 이 글에 나와있는 대부분의 코드는 webpack 공식 문서를 참고함.

## 라이브러리 제작히기
> *Aside from applications, webpack can also be used to **bundle** JavaScript libraries. The following guide is meant for library authors looking to streamline their bundling strategy.*

:arrow_up: 웹팩 공식문서에 나와있는 설명이다

> *A bundle is some related code packaged into a single file.*

> *If you don't want all of your code be put into a single huge bundle you will split it into multiple bundles which are called chunks in webpack terminology. In some cases you will define how your code is split chunks yourself (with an entry that points to multiple files and an output file template like [name].[chunkhash].js), in other cases webpack will do it for you (e.g. with CommonsChunkPlugin).*

> *A module is a JS module (e.g. a CommonJS or an ES6 module). Because internally webpack deals only with modules, all non-js assets are also wrapped in modules. So if you have some .sass files for example, you will import/require them in JS files for them to be bundled, but if you use ExtractTextWebpackPlugin it will output a separate CSS bundle for those files.*

https://stackoverflow.com/questions/42523436/what-are-module-chunk-and-bundle-in-webpack

공식 문서에 나와에 webpack에서 쓰는 bundle같은 용어가 어려운데 스택 오버플로우에 잘 정리해주신 분이 있으니 참고하자.

서두에 있는 공식문서 예제에 보면 목표가 있다.
- 레포에 있는 `lodash`를 번들링 과정에서 제외하기.
- 라이브러리 이름을 `webpack-numbers기로 세팅하기
- 라이브러리 변수 이름을 `webpackNumbers`로 하기
- Node.js에서 접근할 수 있게 하기

예제 저장소를 레포라고 부르겠다.
> *https://github.com/kalcifer/webpack-library-example*

## Expose the Library
라이브러리를 CommonJS, AMD, Node.js등 다양한 환경에서 global variable로 사용하기 위해서 webpack.config.js 파일을 `output`에 있는 `library` 프로퍼티를 수정해주자.

**webpack.config.js**
```javascript
  var path = require('path');

  module.exports = {
    entry: './src/index.js',
    output: {
      path: path.resolve(__dirname, 'dist'),
-     filename: 'webpack-numbers.js'
+     filename: 'webpack-numbers.js',
+     library: 'webpackNumbers'
    },
    externals: {
      lodash: {
        commonjs: 'lodash',
        commonjs2: 'lodash',
        amd: 'lodash',
        root: '_'
      }
    }
  };
```

이제 앞에서 본 것처럼 CommonJS 등 ... 에서 사용할 수 있게 됐다.

사용하는 법과 자세한 내용은 문서를 참고하자
```
 Variable: as a global variable made available by a script tag (libraryTarget:'var').
 This: available through the this object (libraryTarget:'this').
 Window: available trough the window object, in the browser (libraryTarget:'window').
 UMD: available after AMD or CommonJS require (libraryTarget:'umd').
 ```


