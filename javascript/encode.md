# encode

## URL 인코딩

네트워크에서 서로 정보 주고 받기 위해 데이터를 특정 형식으로 변환하는 과정 (URL에서 사용 가능하도록)  
URL에는 아스키 코드로 정의된 128개의 문자만 사용 가능 -> 이 외의 문자들은 인코딩 필요

> URI 전체를 인코딩할 때는 encodeURI()  
> 일부 쿼리 문자열만 인코딩할 때는 encodeURIComponent()

`()` 안에는 string

### encodeURI()

- 인코딩x
  - 알파벳 문자 (A-Z, a-z)
  - 숫자 (0-9)
  - 대시 (-)
  - 밑줄 (_)
  - 마침표 (.)
  - 물결표(~)
  - 콤마 (,)

`&`, `/`, `:`, `?`와 같이 URL에서 기능을 갖는 문자는 인코딩됌    
<-> decodeURI

### encodeURIComponent()

- 인코딩x 
  - 알파벳 문자 (A-Z, a-z)
  - 숫자 (0-9)
  - 대시 (-)
  - 밑줄 (_)
  - 마침표 (.)
  - 물결표(~)
  - 콤마 (,)
  - !, ', (, ), *

위 문자들을 인코딩 하지 않음 -> 단순 쿼리스트링 value 인코딩에 적합  
<-> decodeURIComponent

```javascript
const baseUrl = "https://www.realzu.com/search";

const queryParams = { // 매개변수 추가
    lang: '한국어',
    job: '개발자&학생'
} // 영어는 필요x. '&', 한국어만 인코딩 필요

const queryString = Object.keys(queryParams)
    .map((key) => key + '=' + encodeURIComponent(queryParams[key]))
    .join('&');
// 'lang=%ED%95%9C%EA%B5%AD%EC%96%B4&job=%EA%B0%9C%EB%B0%9C%EC%9E%90%26%ED%95%99%EC%83%9D'

const fullUrl = baseUrl + '?' + queryString;
```
