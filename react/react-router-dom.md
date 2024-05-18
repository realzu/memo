# react-router-dom

> v6.23.1  
> 해당 버전 전후로 완전히 사용법이 바뀌었다.

```javascript
{
  path: '/',
  element: <Root />,
  loader: rootLoader,
  action: rootAction,
}
```

### loader

라우트가 활성화되기 전에 데이터를 가져와 컴포넌트에 전달한다.  
`await` 을 통한 API 비동기 데이터 요청이 가능하다  
데이터 로딩 로직을 라우트 설정에 포함시키기 때문에 컴포넌트 로직이 조금 더 간결해진다.

- useLoaderData
  - 컴포넌트에서 loader 함수의 결과를 받을 수 있다.

```javascript
export async function loader() {
    const contacts = await getContacts()
    return {contacts}
}

export default function Root() {
    const {contacts} = useLoaderData()
```

### action

Form 제출시 실행되는 로직  
Form 역시 react-router-dom 에서 import 해온 것이어야 한다.  
기존에 작성했던 `event.preventDefault()` 로직은 자체적으로 막아주기 때문이 이제 불필요하다.

```javascript
export async function action({request, params}) {...}
```

- request
  - const formData = await request.formData();
  - 여기서 formData는 `Form` tag 안에 있는 `input` tag의 값이며, `name`이 필수적으로 있어야 한다.
  - name에 넣은 값이 객체의 key로 들어온다
  - ex. formData.get("age");
 
- params
  - 바깥 path에 지정해놓은 dynamic segements에 의해 들어온 값이다.
  - path="/projects/:projectId/delete"
  - 여기서 projectId 가 들어오게 되며, params.projectId 로 값을 받아올 수 있다.

### redirect

이름 그대로 다른 곳으로 이동시켜주는 문법이다.

```javascript
export async function action() {
    const contact = await createContact()
    return redirect(`/contacts/${contact.id}/edit`)
}
```
