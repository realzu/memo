# react-router-dom

> v6.23.1  
> 해당 버전 전후로 완전히 사용법이 바뀌었다.

### createBrowserRouter

```javascript
const router = createBrowserRouter([
    {
        path: '/',
        element: <Root />,
        errorElement: <ErrorPage />,
        loader: rootLoader,
        action: rootAction,
        children: [
            { index: true, element: <Index /> },
            {
                path: 'contacts/:contactId',
                element: <Contact />,
                loader: contactLoader,
            },
        ]
    },
])

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <RouterProvider router={router}/>
  </React.StrictMode>,
)
```

### loader

라우트가 활성화되기 전에 데이터를 가져와 컴포넌트에 전달한다. (url이 바뀔 때마다 실행)
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

## Components

### Form

```javascript
<Form action="edit">
    <button type="submit">Edit</button>
</Form>
```

- action
  - Form이 실행될 때 넘어갈 Url 지정 (`<Link to>` 와 비슷하다)
  - `/` 앞에 있으면 해당 도메인에 바로 붙여진다. (ex. `http://localhost:5173/contacts/02hczme/edit`)
  - 없으면 현재 url에 이어서 덧붙여진다. (ex. `http://localhost:5173/edit`)
- onSubmit
  - action과 다르게 `event.preventDefault()` 이 필요하다
- method
  - 일반 HTML's form tag 도 마찬가지로 기본 동작은 'get'
  - get은 Url 쿼리스트링으로 입력한 값이 들어가게 된다

### NavLink

```javascript
<NavLink
  to="/messages"
  className={({ isActive, isPending, isTransitioning }) =>
    [
      isPending ? "pending" : "",
      isActive ? "active" : "",
      isTransitioning ? "transitioning" : "",
    ].join(" ")
  }
>
  Messages
</NavLink>
```

- isActive: 현재 url 과 일치할 때 true
- isPending: 라우트의 loader 함수가 아직 끝나지 않았을 때 true
  - loading spinner 활용 가능
- isTransitioning: 라우트 전환 중인 상태일 때 true
  - 폼 제출 이후 페이지 전환 대기 시 '저장 중' 표시로 활용 가능

## hooks

### useNavigation

```javascript
function SubmitButton() {
  const navigation = useNavigation();

  const text =
    navigation.state === "submitting"
      ? "Saving..."
      : navigation.state === "loading"
      ? "Saved!"
      : "Go";

  return <button type="submit">{text}</button>;
}
```

- state
  - idle: 일반적인 상태. navigaion의 변화가 없을 떄
  - submitting: form 제출이 일어날 때 action 진행시
  - loading: 다음 페이지의 loader 가 일어날 때

### useNavigate

- navigate(value)
  - -1: 뒤로 가기
    - 취소 버튼시 활용 가능
  
### useSubmit

유저의 인터랙션 뿐만 아니라, form 제출 로직을 코드에 추가할 수 있다.
예를 들면, Form tag 안의 input tag의 onChange 함수에 넣게되면, 키보드 입력할 때마다 제출이 가능하다.

- replace
    - 브라우저의 navigation history에 기록되는 설정에 대해 다룬다
    - 기본적으로 push에 따라 새로운 항목으로 추가되지만, `true` 값일 경우 폼 제출 전의 페이지로 바로 이동하게 한다
