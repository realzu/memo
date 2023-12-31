# promise

### promise.all

> 2개 이상의 promise가 비동기적으로 실행되지만, 하나라도 실패할 시 모두가 실패되어야할 경우.

- 프로미스 중 하나라도 실패(reject)하면 모두 실패 처리 (다른 promise가 성공했을지라도)
- 순서대로 실행되지만, 비동기적으로 진행
  - async-await와 다르게 앞의 promise가 `완료`되는 것을 기다리지 않아 빠름

```javascript
const getUserData = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => resolve(1), 300)
    })
}

const getComapnyData = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => reject(new Error('Error!')), 300)
    })
}

const fetchDatas = async () => {
    const [userData, companyData] = await Promise.all([
        getUserData(),
        getCompanyData(),
    ])
    console.log(userData, companyData); // 실패. but 성공시 resolve값 도출
}
```