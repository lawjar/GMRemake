
設計一個馬丁策略的 MQL4 EA程式, 用於 MT4 平台。
要求如下:
part 1) 變數(input variable)要求
Timeframe: 交易時間框架
Bars Counted: 超越多少Bars後入市
Max Buy Order: 最多的馬丁多倉層數, 0為不會開多倉
Max Sell Order: 最多的馬丁空倉層數, 0為不會開空倉
Entry Distance 1: 確認超越前Bars 數多少(points), 開第一層倉
Entry Distance 2: 開第一層倉後, 至少輸多少(points), 才開第二層倉
Entry Distance 3: 開第二層倉後, 至少輸多少(points), 才開第三層倉
Entry Distance 4: 開第三層倉後, 至少輸多少(points), 才開第四層倉
Entry Distance 5: 開第四層倉後, 至少輸多少(points), 才開第五層倉
Entry Distance 6: 開第五層倉後, 至少輸多少(points), 才開第六層倉
Entry Distance 7: 開第六層倉後, 至少輸多少(points), 才開第七層倉
Entry Distance 8: 開第七層倉後, 至少輸多少(points), 才開第八層倉
Lot Size 1: 開第一層倉的手數
Lot Size 2: 開第二層倉的手數
Lot Size 3: 開第三層倉的手數
Lot Size 4: 開第四層倉的手數
Lot Size 5: 開第五層倉的手數
Lot Size 6: 開第六層倉的手數
Lot Size 7: 開第七層倉的手數
Lot Size 8: 開第八層倉的手數
Trend Protection: 預設為 ture, 當true 時, 開第二層以上倉時, 要價格比前一支燭更高或更低, 以保障已經回復順勢才開倉
MACD Trend Protection: 預設為 ture, 當true 時, MACD(14) 連續三支bars背離時不要開倉, 以保障已經回復順勢才開倉
EMA Trend Period (L): 長EMA週期
EMA Trend Filter (L) For Buy: 當高或低於 EMA(L) 時, 才乎合開多倉條件, 可正數或負數表達高於或低於價格多少, 當輸入0時為禁用此參數
EMA Trend Filter (L) For Sell: 當高或低於 EMA(L) 時, 才乎合開空倉條件, 可正數或負數表達高於或低於價格多少, 當輸入0時為禁用此參數
EMA Trend Period (S): 知EMA週期
EMA Trend Filter (S) For Buy: 當高或低於 EMA(L) 時, 才乎合開多倉條件, 可正數或負數表達高於或低於價格多少, 當輸入0時為禁用此參數
EMA Trend Filter (S) For Sell: 當高或低於 EMA(L) 時, 才乎合開空倉條件, 可正數或負數表達高於或低於價格多少, 當輸入0時為禁用此參數
Trailing Points: 超過多少(points)後乎合平倉要求, 開始推高止賺
Stop Trailing Points: 回踩多少(points)後平倉
Slippage in Points: 滑價限度
Spread in Points: 差價限度
Magic Number: EA Magic Number
Comment: EA comment