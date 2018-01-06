---
layout: post
title:  "Lint, Prettier"
author: "Paritta"
---
 
<img src='https://raw.githubusercontent.com/prettier/prettier-logo/master/images/prettier-banner-dark.png'>

`eslint`로 린트를 하는데 자동으로 정리를 하기 위해서 `prettier`를 사용했다.
`prettier`를 `eslint`를 맞췄다. 스타일드 컴포넌트를 린트하기 위해서 `stylelint-processor-styled-components`를 사용했는데 여기서 사용하는 표준 린트가 있는 것 같다. 굳이 커스터마이징 하고 싶지 않아서 그대로 쓸려다 보니까 styled linter에 `eslinter`를 맞춰 줘야했다. `eslint`를 고치려니까 `prettier`를 또 `eslint`에 맞춰줘야 한다. indent를 space랑 tab이랑 구분해야 되는거 진자 귀찮허당

```
// eslint
"indent": [
            "error",
            2
        ],
// prettier
"--use-tabs": false,
```

다음에 참고하기 위해서 메모~~~~~
