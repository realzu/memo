# URL

Uniform Resource Locators  
웹에서 주어진 고유 리소스 주소(HTML 페이지, CSS 문서, 이미지 등)

## URL 구조

![image](https://github.com/realzu/memo/assets/97022695/def441b1-af20-4f4a-a6ea-c1a43a954f7e)

> https://blog.realzu.com:80/post?no=123#conatiner

`https`: 프로토콜(protocol)  
`blog`: 서브도메인  
`realzu.com`: 도메인  
`80`: 포트  
`post`: Path (Subdirectory)  
`no=123`: 쿼리스트링(Querystring). parameter  
`#container`: Anchor  

### Schema(Protocol)

브라우저가 서버에 리소스 요청하기 위해 사용해야 하는 프로토콜  
(프로토콜은 컴퓨터 내부 또는 컴퓨터간 데이터의 교환 방식을 정의하는 규칙 체계. 데이터의 내용을 그대로 받아오기 위함)  

- HTTP: Hyper Text Transfer Protocol
- HTTPS: Hyper Text Transfer Protocol Secure
- ftp: 파일 송수신 위한 프로토콜
- mailto: 전자메일

### Domain Name

도메인은 요청하는 웹 서버를 나타낸다.  
IP주소로도 사용 가능하지만 일반적으로 네임서버를 통해 변환해서 사용한다.  

- 서브 도메인
  - `www.`, `m.`
  - 호스트 또는 서브도메인
- 도메인 이름
  - `google`, `naver`
  - 주로 서비스명으로 도메인명을 지정
- 최상위 도메인
  - `.com`, `.co.kr`
  - 국가, 목적, 종류 등을 나타냄

### Port

- 포트 번호를 통해 어떤 서버를 이용할지 결정
- HTTP(80), HTTPS(443) -> HTTP 프로토콜의 표준 포트일 경우, 일반적으로 생략

### Path

웹 서버에 있는 리소스 경로

### Parameter

- `?no=123&page=3`
- 파라미터 or 쿼리스트링
- `?` 뒤에 나열 및 `&`로 key-value 연결

### Anchor

- Anchor or Fragment
- 특정 요소 지정 가능 (일종의 '책갈피' 역할 -> 해당 지점의 콘텐츠 표시)
- ex. id를 지정하면 해당 영역으로 바로 스크롤되어 이동
- 서버로 전송되지 않는다는 점.

---

## new URL

url 객체를 생성하거나 다루기 위한 API

- searchParams
  - new URL(request.url).searchParams
  - url에 대한 파라미터 제공
  - size, get, set()...
  - new URLSearchParams 와 쿼리스트링을 다루는 부분은 같다
