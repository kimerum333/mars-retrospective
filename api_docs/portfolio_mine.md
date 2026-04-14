
# 내 종목 간략목록보기 ✔️
- 왼쪽 사이드바의 내 종목 목록보기에 쓰기 위해 사용
## 요청
```
method: GET
endpoint: /api/portfolios/list
제약 조건 : 로그인 필수
```

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "your stock list",
  "data": [
    {
      "symbol": "A",
      "name": "Agilent Technologies, Inc.",
      "currentPrice": 111.84,
      "priceDelta": -0.0799999999999983
    },
    {
      "symbol": "AAPL",
      "name": "Apple Inc.",
      "currentPrice": 200.66,
      "priceDelta": -0.18999999999999773
    }
  ]
}
```
### 응답 파라미터
- symbol: 심볼
- currentPrice: 현재가격
- priceDelta: 전날 종가 대비 현재 가격


# 통합 포트폴리오 조회 ✔️
- 회원 개인의 전체적인 주식투자 성과를 조회
## 요청
```
method: GET
endpoint: /api/portfolios/overall
제약 조건 : 로그인 필수
```

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "this is your simple user PF!",
  "data": {
    "totalAsset": 105321.82,
    "investedAmount": 719.82,
    "evalGain": 9,
    "returnRate": 0.01250312578144536,
    "totalSeed": 105206,
    "investRatio": 0.006842005208828395,
    "cash": 104593
  }
}
```
### 응답 파라미터
- totalAsset: 총자산
- investedAmount: 투자금액
- evalGain: 평가손익
- returnRate: 수익률
- totalSeed: 시드머니
- investRatio: 총 투자비율
- cahs: 현금자산

# 주식종목별 포트폴리오 조회 ✔️
- 보유중인 각 주식별 투자성과를 조회
## 요청
```
method: GET
endpoint: /api/portfolios/stock
제약 조건 : 로그인 필수
```

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "this is your stock PF!",
  "data": [
    {
      "symbol": "AAPL",
      "name": "Apple Inc.",
      "quantity": 3,
      "avgBuyPrice": 202.66,
      "evalAmount": 616.98,
      "evalGain": 9,
      "returnRate": 0.014803118523635646
    },
    {
      "symbol": "A",
      "name": "Agilent Technologies, Inc.",
      "quantity": 1,
      "avgBuyPrice": 111.84,
      "evalAmount": 111.84,
      "evalGain": 0,
      "returnRate": 0
    }
  ]
}
```
### 응답 파라미터
- avgBuyPrice: 평균단가
- evalAmount: 평가금액
- evalGain: 평가손익
- returnRate: 수익률



# 주식 거래내역 조회 ✔️
- 매수 또는 매도를 진행 했던 내역을 조회
## 요청
```
method: GET
endpoint: /api/portfolios/history
제약 조건 : 로그인 필수
```

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "this is your stock trade history!",
  "data": [
    {
      "symbol": "AAPL",
      "name": "Apple Inc.",
      "quantity": 3,
      "currentPrice": 202.66,
      "date": "2025-06-07T05:41:26.709Z",
      "returnRate": 0.0148031185
    },
    {
      "symbol": "MSFT",
      "name": "Microsoft Corporation",
      "quantity": 1,
      "currentPrice": 470.16,
      "date": "2025-06-08T14:21:36.709Z",
      "returnRate": 0.0112321212
    }
  ]
}
```
### 응답 파라미터
- currentPrice: 거래단가
- quantity: 수량
- returnRate: 수익률

