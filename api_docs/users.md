# 회원 기능
## 회원가입
- method: POST
- endpont: http://{server}:4000/users/signup
- header: Content-Type: application/json
- body: 
```
{
    "email":"elon@mars.com",
    "password":"wegomars",
    "nick":"doge1"
}
```

- response: 200
```
{
    "success": "true",
    "message": "User registered successfully.",
    "data": {
        "id": 1,
        "email": "elon@mars.com",
        "nick": "doge1"
    }
}
```

- response: 400 실패시1 (이메일 중복)
```
{
    "success": "false",
    "message": "Email already in use."
}
```

- response: 400 실패시2 (param 값 누락)
```
{
    "success": "false",
    "message": "Invalid request body. Email, password, and nick are required."
}
```

## 비밀번호 초기화 (authentication) 
- method: POST
- endpont: http://{server}:4000/users/resetpwd
- header: Content-Type: application/json
- body: 
```
{
    "email":"elon@mars.com",
    "code":"0000"
}
```
- response: 200
```
{
    "success": "true",
    "message": "Authentication successful. You can reset your password."
}
```
- response: 400 실패시1(인증번호 X)
```
{
    "success": "false",
    "message": "The verification code does not match."
}
```
- response: 400 실패시2 (이메일 X)
```
{
    "success": "false",
    "message": "No user is registered with the provided email."
}
```

## 로그인
- method: POST
- endpoint: http://{server}:4000/users/login
- header: Content-Type: application/json
- body:
```
{
    "email": "elon@mars.com",
    "password": "wegomars"
}
```
- response: 200
```
{
    "success": "true",
    "message": "Login successful."
}
```
- response: 400(입력 누락)
```
{
    "success": "false",
    "message": "Email and password are required."
}
```
- response: 401(입력 불일치)
```
{
    "success": "false",
    "message": "Invalid email or password."
}
```

## 로그아웃
- method: GET
- endpoint: http://{server}:4000/users/logout
- response: 200 OK (로그아웃 성공)
```
{  
    "success": "true",
    "message": "Logout successful."
}
```
- response: 401 Unauthorized (세션 없음 또는 만료)
```
{
    "success": "false",
    "message": "Unauthorized request."
}
```