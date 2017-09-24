---
layout: post
title:  "[Webpack탐방기]Authoring Library"
author: "Paritta"
---

<<<<<<< HEAD:_posts/2017-09-28-[Webpack탐방기]Autohring Library.1.md
<<<<<<< HEAD:_posts/2017-09-28-[Webpack탐방기]Autohring Library.1.md
<img src="https://cdn-images-1.medium.com/max/1920/1*gdoQ1_5OID90wf1eLTFvWw.png">
=======
<img src="https://www.google.co.kr/search?q=webpack&source=lnms&tbm=isch&sa=X&ved=0ahUKEwiw663E88fWAhWGabwKHSJZB7kQ_AUICygC&biw=1745&bih=915#imgrc=tf-2ha3fypZlMM:">
>>>>>>> 6a18c62... 1:_posts/2017-09-28-[Webpack탐방기]Autohring Library.md
=======
<img src="https://cdn-images-1.medium.com/max/1920/1*gdoQ1_5OID90wf1eLTFvWw.png">
>>>>>>> 135f2ab... 1:_posts/2017-09-28-[Webpack탐방기]Autohring Library.md

# [Webpack탐방기]Authoring Library 
[*https://webpack.js.org/guides/author-libraries/*](https://webpack.js.org/guides/author-libraries/)

> 이 글에 나와있는 대부분의 코드는 webpack 공식 문서를 참고함

## 라이브러리 제작히기
> *Aside from applications, webpack can also be used to `bundle` JavaScript libraries. The following guide is meant for library authors looking to streamline their bundling strategy.*

- *웹팩 공식문서에 나와있는 설명이다.*

> *A bundle is some related code packaged into a single file.*

> *If you don't want all of your code be put into a single huge bundle you will split it into multiple bundles which are called chunks in webpack terminology. In some cases you will define how your code is split chunks yourself (with an entry that points to multiple files and an output file template like [name].[chunkhash].js), in other cases webpack will do it for you (e.g. with CommonsChunkPlugin).*

> *A module is a JS module (e.g. a CommonJS or an ES6 module). Because internally webpack deals only with modules, all non-js assets are also wrapped in modules. So if you have some .sass files for example, you will import/require them in JS files for them to be bundled, but if you use ExtractTextWebpackPlugin it will output a separate CSS bundle for those files.*

[*https://stackoverflow.com/questions/42523436/what-are-module-chunk-and-bundle-in-webpack*](https://stackoverflow.com/questions/42523436/what-are-module-chunk-and-bundle-in-webpack)

공식 문서에 나와에 webpack에서 쓰는 bundle같은 용어가 어려운데 스택 오버플로우에 잘 정리해주신 분이 있으니 참고하자.

서두에 있는 공식문서 예제에 보면 목표가 있다.
- 레포에 있는 `lodash`를 번들링 과정에서 제외하기.
- 라이브러리 이름을 `webpack-numbers`로 세팅하기
- 라이브러리 변수 이름을 `webpackNumbers`로 하기
- Node.js에서 접근할 수 있게 하기

*예제 저장소를 레포라고 부르겠다.*

[*https://github.com/kalcifer/webpack-library-example*](https://github.com/kalcifer/webpack-library-example)

## Externalize Lodash
웹팩을 실행시켜보면 번들에 lodash가 포함되어 있다고 한다고 한다. (실행 안시켜봄. 다음부터는 해봐야지 >..<)이 경우에, lodash를 `peerDependency`라고 한다. 사용자는 lodash를 이미 설치해서 또 설치할 필요가 없는데, 웹팩은 lodash를 번들에 포함시킨다. 성능 문제로 귀결될 가능성이 높다.

공식 문서를 참고해서, `externals`프로퍼티를 설정한다.

**webpack.config.js**
```javascript
var path = require('path');

  module.exports = {
    entry: './src/index.js',
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: 'webpack-numbers.js'
-   }
+   },
+   externals: {
+     lodash: {
+       commonjs: 'lodash',
+       commonjs2: 'lodash',
+       amd: 'lodash',
+       root: '_'
+     }
+   }
  };
```

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
 - Variable: as a global variable made available by a script tag (libraryTarget:'var').
 - This: available through the this object (libraryTarget:'this').
 - Window: available trough the window object, in the browser (libraryTarget:'window').
 - UMD: available after AMD or CommonJS require (libraryTarget:'umd').
 ```

라이브러리가 신비해보이기만 했었다. 문서를 보니 예제를 포크해서 요리조리 고치면 라이브러리도 만들어 볼 수 있을것 같다.

