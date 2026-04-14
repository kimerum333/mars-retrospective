# 유저 선호 추가 ✔️
- ai추천에 사용하기 위해 유저의 개인화된 선호를 입력받아 db에 저장하기 위한 api
- upsert 기반으로 동작(없으면 만들고, 재요청시 업데이트함)
## 요청
```
method: POST
endpoint: /api/ai/preference
header: Content-Type: application/json
제약 조건 : 로그인 필수
```
- body: 
```JSON
{
  "riskLevel": "high",
  "preferredStrategies": ["dividend_stability", "portfolio_balance", "value_stability", "momentum", "sector_rotation", "rebound_buy"],
  "preferredSectors" : ["Basic Materials", "Communication Services", "Consumer Cyclical", "Consumer Defensive", "Energy", "Financial Services", "Healthcare", "Industrials", "Real Estate", "Technology", "Utilities" ]
}
```
## 요청 파라미터
- riskLevel : high 나 low 중 1택.
- preferredStrategies : 위 예시에 나온 6중 n 택(최소 0)
- preferredSectors : 위 예시에 나온 11중 n 택(최소 0)

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "user preference saved!",
  "data": {
    "riskLevel": "high",
    "preferredStrategies": [
      "dividend_stability",
      "portfolio_balance",
      "value_stability",
      "momentum",
      "sector_rotation",
      "rebound_buy"
    ],
    "preferredSectors": [
      "Basic Materials",
      "Communication Services",
      "Consumer Cyclical",
      "Consumer Defensive",
      "Energy",
      "Financial Services",
      "Healthcare",
      "Industrials",
      "Real Estate",
      "Technology",
      "Utilities"
    ],
    "createdAt": "2025-06-09T15:59:48.324Z",
    "updatedAt": "2025-06-09T17:57:23.000Z"
  }
}
```



# 내 선호 조회 ✔️
## 요청
```
method: GET
endpoint: /api/ai/preference
제약 조건 : 로그인 필수
```

## 응답
- response: 200
```JSON
{
  "success": true,
  "message": "this is your user preference",
  "data": {
    "riskLevel": "high",
    "preferredStrategies": [
      "dividend_stability",
      "portfolio_balance",
      "value_stability",
      "momentum",
      "sector_rotation",
      "rebound_buy"
    ],
    "preferredSectors": [
      "Basic Materials",
      "Communication Services",
      "Consumer Cyclical",
      "Consumer Defensive",
      "Energy",
      "Financial Services",
      "Healthcare",
      "Industrials",
      "Real Estate",
      "Technology",
      "Utilities"
    ],
    "createdAt": "2025-06-09T15:59:48.324Z",
    "updatedAt": "2025-06-09T17:57:23.000Z"
  }
}
```
### 응답 파라미터
- symbol: 심볼
- createdAt: 만들어진 날짜
- currentPrice: 현재가격
- priceDelta: 전날 종가 대비 현재 가격


# AI 추천 ✔️
## 요청
```
method: GET
endpoint: /api/ai/recommend
제약 조건 : 
1. 로그인이 되어 있을 것.
2. 지갑이 만들어져 있을 것.
3. 종목을 뭐라도 샀을 것.
4. 유저 선호를 입력했을 것(전략 고르는데 도움이 많이 됨)
```

## 응답
```json
{
  "success": true,
  "message": "AI answer",
  "data": {
    "stocks": [
      {
        "symbol": "NVDA",
        "name": "NVIDIA Corporation",
        "sector": "Technology",
        "industry": "Semiconductors",
        "score": 31,
        "metrics": [
          { "name": "sector_trend_score", "value": 8.31, "score": 5 },
          { "name": "price_change_1m", "value": 17.04, "score": 2.56 },
          { "name": "volatility", "value": 2.09, "score": 0.84 }
        ],
        "reasons": [
          {
            "type": "strategy",
            "detail": "Sector Rotation 전략: 사용자의 리스크 허용 수준이 'high'이고, 보유 섹터와 선호 섹터 간 불일치가 존재하므로 유망한 섹터로 포지션을 옮기는 전략이 적합합니다.",
            "score": 15
          },
          {
            "type": "strategy",
            "detail": "Rebound Buy 전략: 사용자의 리스크 허용 수준이 'high'이며, S&P500의 최근 12개월 평균 수익률이 양호하여 하락한 종목 중 반등 가능성이 있는 종목을 선별하는 전략이 유리할 수 있습니다.",
            "score": 16
          },
          {
            "type": "commentary",
            "detail": "NVIDIA는 Technology 섹터의 강력한 성장세를 바탕으로 포트폴리오의 섹터 다변화에 기여할 수 있습니다. 최근 가격 상승 추세가 강하지만, 변동성이 다소 높아 주의가 필요합니다."
          }
        ]
      },
      {
        "symbol": "GILD",
        "name": "Gilead Sciences, Inc.",
        "sector": "Healthcare",
        "industry": "Drug Manufacturers - General",
        "score": 20,
        "metrics": [
          { "name": "beta", "value": 0.282, "score": 2.15 },
          { "name": "current_ratio", "value": 1.369, "score": 0.17 },
          { "name": "roe", "value": 0.317, "score": 2.5 },
          { "name": "preferred_sector_score", "value": 1, "score": 0.15 },
          { "name": "underweighted_sector_score", "value": 1, "score": 0.1 }
        ],
        "reasons": [
          {
            "type": "strategy",
            "detail": "Portfolio Balance 전략: 사용자의 리스크 허용 수준이 'high'이며, 투자 비중이 매우 낮고 특정 섹터에 편중되어 있어 자산 리밸런싱을 통해 안정성을 높이는 것이 필요합니다.",
            "score": 20
          },
          {
            "type": "commentary",
            "detail": "Gilead Sciences는 Healthcare 섹터로의 리밸런싱을 통해 포트폴리오의 안정성을 높일 수 있습니다. 낮은 베타값은 시장 변동성에 대한 방어력을 제공할 수 있습니다."
          }
        ]
      },
      {
        "symbol": "TXN",
        "name": "Texas Instruments Incorporated",
        "sector": "Technology",
        "industry": "Semiconductors",
        "score": 20,
        "metrics": [
          { "name": "beta", "value": 0.955, "score": 1.31 },
          { "name": "current_ratio", "value": 5.258, "score": 0.66 },
          { "name": "roe", "value": 0.288, "score": 2.4 },
          { "name": "preferred_sector_score", "value": 1, "score": 0.15 },
          { "name": "underweighted_sector_score", "value": 1, "score": 0.1 }
        ],
        "reasons": [
          {
            "type": "strategy",
            "detail": "Portfolio Balance 전략: 사용자의 리스크 허용 수준이 'high'이며, 투자 비중이 매우 낮고 특정 섹터에 편중되어 있어 자산 리밸런싱을 통해 안정성을 높이는 것이 필요합니다.",
            "score": 11
          },
          {
            "type": "strategy",
            "detail": "Rebound Buy 전략: 사용자의 리스크 허용 수준이 'high'이며, S&P500의 최근 12개월 평균 수익률이 양호하여 하락한 종목 중 반등 가능성이 있는 종목을 선별하는 전략이 유리할 수 있습니다.",
            "score": 9
          },
          {
            "type": "commentary",
            "detail": "Texas Instruments는 높은 ROE를 통해 강력한 수익성을 보이며, Technology 섹터로의 다변화를 지원합니다. 다소 높은 베타값은 시장 변동성에 민감할 수 있으니 주의가 필요합니다."
          }
        ]
      },
      {
        "symbol": "SMCI",
        "name": "Super Micro Computer, Inc.",
        "sector": "Technology",
        "industry": "Computer Hardware",
        "score": 20,
        "metrics": [
          { "name": "sector_trend_score", "value": 8.31, "score": 5 },
          { "name": "price_change_1m", "value": 28.01, "score": 3 },
          { "name": "volatility", "value": 5.82, "score": 2 }
        ],
        "reasons": [
          {
            "type": "strategy",
            "detail": "Sector Rotation 전략: 사용자의 리스크 허용 수준이 'high'이고, 보유 섹터와 선호 섹터 간 불일치가 존재하므로 유망한 섹터로 포지션을 옮기는 전략이 적합합니다.",
            "score": 20
          },
          {
            "type": "commentary",
            "detail": "Super Micro Computer는 Technology 섹터의 긍정적인 트렌드를 활용하여 포트폴리오의 성장 잠재력을 높일 수 있습니다. 최근 가격 변동성이 크므로, 리스크 관리가 중요합니다."
          }
        ]
      }
    ]
  }
}

```

