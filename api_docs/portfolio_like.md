# 관심종목 추가 ✔️
## 요청
```
method: POST
endpoint: /api/portfolios/like
header: Content-Type: application/json
제약 조건 : 로그인 필수
```
- body: 
```JSON
{
    "symbol" : "TSLA"
}
```
## 요청 파라미터
- symbol : 관심종목에 추가하려는 주식

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "you liked TSLA succesfully",
  "data": {
    "symbol": "TSLA",
    "createdAt": "2025-06-08T07:01:32.609Z"
  }
}
```
### 응답 파라미터
- symbol: 심볼
- createdAt: 만들어진 날짜

## 에러 응답
1. 이미 좋아요한 주식을 또 좋아요하려고 함
- response: 400
```JSON
{
  "success": false,
  "message": "you already liked this stock!"
}
```

# 관심종목 삭제 ✔️
## 요청
```
method: DELETE
endpoint: /api/portfolios/like
header: Content-Type: application/json
제약 조건 : 로그인 필수
```
- body: 
```JSON
{
    "symbol" : "TSLA"
}
```
## 요청 파라미터
- symbol : 관심종목에 추가하려는 주식

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "you disliked TSLA succesfully",
  "data": true
}
```

## 에러 응답
1. 이미 좋아요에서 뺀 종목을 또 빼려고 함
-response: 400
```JSON
{
  "success": false,
  "message": "no such like"
}
```


# 내 관심종목 목록보기 ✔️
## 요청
```
method: GET
endpoint: /api/portfolios/like
제약 조건 : 로그인 필수
```

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "your likes successfully listed",
  "data": [
    {
      "symbol": "TSLA",
      "name": "Tesla, Inc.",
      "sector": "Consumer Cyclical",
      "industry": "Auto Manufacturers",
      "currentPrice": 295.125,
      "priceDelta": -51.33499999999998
    },
    {
      "symbol": "AAPL",
      "name": "Apple Inc.",
      "sector": "Technology",
      "industry": "Consumer Electronics",
      "currentPrice": 203.93,
      "priceDelta": 3.0800000000000125
    }
  ]
}
```
### 응답 파라미터
- symbol: 심볼
- createdAt: 만들어진 날짜
- currentPrice: 현재가격
- priceDelta: 전날 종가 대비 현재 가격