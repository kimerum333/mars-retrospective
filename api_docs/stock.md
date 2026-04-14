
# 차트 데이터 조회 ✔️
- 캔들차트를 뽑기 위한 데이터를 요청
```
method: GET
endpoint: /api/stocks/chart?symbol={symbol}&interval={interval}&limit={limit}
parameters:
symbol: 종목 코드 (예: AAPL)
interval: 차트 기간 (1h,1day,1week,1month)
limit:몇 개의 ohlcv 데이터를 가져올지(data 의 length 를 결정). 최대값은 120.
```

- response: 200
- 정렬 : 최신이 늘 data[0]
```JSON
{
    "success": true,
    "message": "AAPL's chart data",
    "data": [
        {
            "timestamp": "2025-05-30",
            "open": 199.37,
            "high": 201.96,
            "low": 196.78,
            "close": 200.85,
            "volume": 70753100
        },
        {
            "timestamp": "2025-05-29",
            "open": 203.58,
            "high": 203.81,
            "low": 198.51,
            "close": 199.95,
            "volume": 51396800
        }
    ]
}
```
- response: 400 (잘못된 기간 파라미터)
```JSON
{
  "success": false,
  "message": [
    "interval must be one of: 1hour, 1day, 1week, 1month"
  ]
}
```

- response: 404 (해당 심볼 없음)
```JSON
{
  "success": false,
  "message": "No Such Symbol : (AAPd)"
}
```
# 종목 상세 정보 조회 ✔️
- 정확한 심볼 정보를 req, 자세한 주식종목정보를 res 
```
method: GET
endpoint: /api/stocks/{symbol}
parameters:
symbol: 종목 코드 (예: AAPL)
```

- response: 200
```JSON
{
  "success": true,
  "message": "AAPL's detailed data",
  "data": {
    "stockId": 2,
    "symbol": "AAPL",
    "name": "Apple Inc.",
    "roe": 1.51306,
    "eps": 6.48883,
    "bps": 4.45482,
    "beta": 1.275,
    "marketCap": 2999860000000,
    "dividendYield": 0.00502863,
    "currentRatio": 0.82087,
    "debtRatio": 1.46994,
    "sector": "Technology",
    "industry": "Consumer Electronics",
    "lastPrice": 200.85,
    "currentPrice": 200.66
  }
}
```

- response: 404 (해당 심볼 없음)
```JSON
{
  "success": false,
  "message": "No Such Symbol : (AAPd)"
}
```

# 주식 종목 검색 ✔️
-심볼 문자열의 일부를 req, 해당 문자열을 이름 or symbol에 포함한 주식을 최대 limit 개 배열에 담아 res

```
method: GET
endpoint: /api/stocks/search?query={query}&limit={limit}
```
```
query : 검색 조건이 될 문자열(심볼, 네임 어느쪽이든 가능, 아래는 AA로 검색한 예시)
limit : 숫자, 최대 20건
```

- response: 200
```JSON
{
  "success": true,
  "message": "search succesful",
  "data": [
    {
      "symbol": "A",
      "name": "Agilent Technologies, Inc.",
      "sector": "Healthcare",
      "industry": "Diagnostics & Research",
      "currentPrice": 114.97,
      "priceDelta": 3.049999999999997,
      "hourlyVolume": 55892
    },
    {
      "symbol": "AAPL",
      "name": "Apple Inc.",
      "sector": "Technology",
      "industry": "Consumer Electronics",
      "currentPrice": 202.84,
      "priceDelta": 1.990000000000009,
      "hourlyVolume": 266878
    }
  ]
}
```
```
pricedelta : 어제 종가 - 현재가. 주식정보 제공 사이트들은 보통 어제 종가 대비 얼마나 변화했나를 퍼센트로 나타낸다고 한다. 만약 퍼센트로 표시하고 싶다면 계산이 필요.
hourlyVolume : 최근 1시간 이내 거래량
```

```
- response: 400 (검색어 누락)
{
    "success": false,
    "message": "Search query parameter is required"
}
```



# 주식 목록 조회 ✔️(반만 완성)
-핫한 종목, 내 종목, 내 관심종목 의 3가지 옵션에 따라 목록을 반환.
```
method: GET
endpoint: /api/stocks/list?option={option}&limit={limit}
```
```
option : [hot,owned,liked] 3중 1택 (현재 HOT만 완성)
limit : 숫자, 최대 20건
```

- response: 200
```JSON
{
  "success": true,
  "message": "listing succesful",
  "data": [
    {
      "symbol": "T",
      "name": "AT&T Inc.",
      "sector": "Communication Services",
      "industry": "Telecom Services",
      "currentPrice": 27.37,
      "priceDelta": -0.4299999999999997,
      "hourlyVolume": 5288960
    },
    {
      "symbol": "DFS",
      "name": "Discover Financial Services",
      "sector": "Financial Services",
      "industry": "Credit Services",
      "currentPrice": 200.21,
      "priceDelta": 0.1599999999999966,
      "hourlyVolume": 3716820
    },
    {
      "symbol": "WFC",
      "name": "Wells Fargo & Company",
      "sector": "Financial Services",
      "industry": "Banks - Diversified",
      "currentPrice": 75.39,
      "priceDelta": 0.6099999999999994,
      "hourlyVolume": 3550730
    },
    {
      "symbol": "VZ",
      "name": "Verizon Communications Inc.",
      "sector": "Communication Services",
      "industry": "Telecom Services",
      "currentPrice": 43.25,
      "priceDelta": -0.7100000000000009,
      "hourlyVolume": 3069330
    },
    {
      "symbol": "XOM",
      "name": "Exxon Mobil Corporation",
      "sector": "Energy",
      "industry": "Oil & Gas Integrated",
      "currentPrice": 102.305,
      "priceDelta": 0.005000000000009663,
      "hourlyVolume": 2756710
    }
  ]
}
```
```
pricedelta : 어제 종가 - 현재가. 주식정보 제공 사이트들은 보통 어제 종가 대비 얼마나 변화했나를 퍼센트로 나타낸다고 한다. 만약 퍼센트로 표시하고 싶다면 계산이 필요.
hourlyVolume : 최근 1시간 이내 거래량
```