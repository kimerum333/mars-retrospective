# 주식 구매 ✔️
## 요청
```
method: POST
endpoint: /api/trades/buy
header: Content-Type: application/json
제약 조건 : 로그인 필수
```
- body: 
```JSON
{
    "symbol" : "AAPL",
    "quantity" : 1,
    "price" : "203.96"
}
```
## 요청 파라미터
- symbol : 구입하려는 주식
- quantity : 구입하려는 수량(최대1000000,백만)
- price : 구입하려는 주식의 개당 가격 (stock 의 종목 상세 정보 조회 api에서 미리 받아뒀어야 함)



## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "buy successful",
  "data": {
    "symbol": "AAPL",
    "price": 203.96,
    "balance": 99796.04,
    "share": 1,
    "tradedAt": "2025-06-07T05:41:26.709Z"
  }
}
```
### 응답 파라미터
- share: 구매 후 해당 주식 보유 수
- balance: 구매 후 계좌 잔고
- tradeAt: 구매 체결 시점

## 에러 응답
1. 클라이언트가 주식가격을 받아온 시점의 주식가격이, 서버의 주식 가격과 다름
```JSON
{
  "success": false,
  "message": "the stock price changed. please request again with new price"
}
```
2. 지갑의 금액보다 더 많이 사려고 함
```JSON
{
  "success": false,
  "message": "not enough money in your wallet!"
}
```



# 주식 판매 ✔️
## 요청
```
method: POST
endpoint: /api/trades/sell
header: Content-Type: application/json
제약 조건 : 로그인 필수
```
- body: 
```JSON
{
    "symbol" : "AAPL",
    "quantity" : 1,
    "price" : "203.96"
}
```
## 요청 파라미터
- symbol : 판매하려는 주식
- quantity: 판매하려는 수량(최대 1000000, 백만)
- price: 판매하려는 주식의 개당 가격 (stock 의 종목 상세 정보 조회 api에서 미리 받아뒀어야 함)
##



## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "sell successful",
  "data": {
    "symbol": "AAPL",
    "price": 203.96,
    "balance": 99999.96,
    "share": 0,
    "tradedAt": "2025-06-07T05:55:13.321Z"
  }
}
```
## 응답 파라미터
- share: 판매 후 해당 주식 보유 수
- balance: 판매 후 잔고
- tradeAt: 판매 체결 시점

## 에러 응답
1. 가진 주식수보다 더 많이 팔려고 할 때
```JSON
{
  "success": false,
  "message": "You have only 0 share"
}
```
