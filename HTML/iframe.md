# iframe

inline frame의 약자  
페이지 안에 다른 html 파일을 불러오는 기능  
영상, 지도 등의 외부 요소를 삽입할 때 주로 사용  

### 사용법

`<iframe>` Tag  
src: 삽입할 웹 문서 경로  
width, height로 창 크기 조절  
지원하지 않는 브라우저는 태그 안에 text로 표현 가능 (Ex. `<img>`의 alt)  
이 외에도 style 등의 여러 속성 존재 (HTML5와 속성 달라 조심)   

```javascript
<iframe src="https://www.realzu.com" width="300px" height="200px">
    <p>해당 브라우저는 iframe을 지원하지 않습니다</p>
</iframe>
```

### 주의점

> XSS (cross site scripting) 보안 이슈

서비스 공급자가 http header를 통해 페이지 도메인과 iframe 도메인을 비교하여  
다를 경우, 에러 (`refused to connnect`) 리턴할 수 있음

html5 이후 권장되지는 않는다고 함!

[HTML iframe 태그 by TCP SCHOOL](https://tcpschool.com/html-tags/iframe)