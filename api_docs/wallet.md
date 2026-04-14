
# 초기 지갑 작성 ✔️
- 갓 가입한 회원이라 지갑이 아직 생성되지 않은 경우, 초기 시드머니를 amount 만큼 지금한 지갑을 만들어준다.
```
method: POST
endpoint: /api/wallets
header: Content-Type: application/json
parameters:
amount: 지급할 초기 자금(달러 기준), 음수 가능, 최대 100000(십만달러), 최소 -100000(십만달러)


제약 조건 : 로그인 필수
```
- body: 
```JSON
{
    "amount": 100000
}
```

- response: 200
```JSON
{
  "success": true,
  "message": "create wallet success",
  "data": {
    "email": "elon8@mars.com",
    "nick": "doge1",
    "updatedAt": "2025-06-05T00:40:16.666Z",
    "cyberDollar": 100000
  }
}
```
- response: 401 (로그인 없을 시)
```JSON
{
  "success": false,
  "message": "로그인이 필요합니다"
}
```


# 내 지갑 확인 ✔️
- 현재 내가 가진 현금량을 리턴
```
method: GET
endpoint: /api/wallets
header: Content-Type: application/json

제약 조건 : 로그인 필수
```

- response: 200
```JSON
{
  "success": true,
  "message": "get wallet success",
  "data": {
    "email": "elon8@mars.com",
    "nick": "doge1",
    "cyberDollar": 100000,
    "updatedAt": "2025-06-05T00:40:16.666Z"
  }
}
```
- response: 400 (지갑이 없을 시)
```JSON
{
  "success": false,
  "message": "this user have no wallet!"
}
```


# 지갑 잔고 변경 확인 ✔️
- 내 현재 지갑의 잔고에 +amount(음수 가능)
```
method: PUT
endpoint: /api/wallets

parameters:
amount: 최대 100000(십만달러), 최소 -100000(십만달러)

제약 조건 : 로그인 필수
```
- body: 
```JSON
{
    "amount": 100000
}
```


- response: 200
```JSON
{
  "success": true,
  "message": "wallet updated successfully",
  "data": {
    "updatedAt": "2025-06-05T00:51:39.000Z",
    "cyberDollar": 155000
  }
}
```
- response: 400 (지갑이 없을 시)
```JSON
{
  "success": false,
  "message": "this user have no wallet!"
}
```
