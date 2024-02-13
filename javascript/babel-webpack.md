# Babel 그리고 Webpack

# Babel

> Javascript Compiler  
> ES6+ 버전 이상의 자바스크립트를 변환하여 구형 브라우저에서도 동작시키는 트랜스파일러

Javascript의 표준인 ECMAScript는 매년 새로운 버전이 출시된다.  
ES6(ES2015) 이후로 ESNext는 구형 브라우저와 호환이 되지 않을 수 있다.  
계속해서 버전 Up이 되고 있는 자바스크립트가 모든 브라우저에서 작동될 수 있도록  
`Babel`은 ES6를 ES5 문법으로 소스코드를 *변환*해준다.

Babel을 node 환경에서만 동작시키면 문제가 없지만 브라우저에서 실행하면 에러가 난다.  
node.js는 CommonJS 방식의 모듈 로딩 시스템.  
but, 브라우저는 CommonJS 방식의 require 함수를 지원하지 않는다!  
-> Webpack을 통해 문제 해결 가능

# Webpack

> 모듈 번들러  
> HTML, CSS, 자바스크립트, 이미지 등의 여러 리소스들을 하나로 번들링

하나의 시작점(entry point)으로 부터 의존적인 모듈을 모두 찾아 하나의 파일로 만든다 -> 결과물 = Output  

- 왜 사용할까?
  - 여러 개의 자바스크립트 파일을 하나로 번들링
    - -> HTML에서 일일이 <script>태그로 JS파일 로드할 필요 없음
    - -> 파일이 많아질수록 http 통신 병목현상 발생 가능한데, 하나로 로드

- webpack.config.js
  - webpack이 실행될 때 참조하는 설정 파일 (최상단)
