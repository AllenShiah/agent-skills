---
name: stock-analysis
description: "Runs a 7-step fundamental research SOP before buying a stock, using free public data in about 30 minutes: business mix, gross margin, capex, inventory, institutional positioning, goodwill, then price. Use when the user wants to analyze, research, or evaluate a stock, or asks what to check before buying. Use the English version for US stocks or English-language materials; use the Chinese version (中文版) for Taiwan stocks. 買股前的基本面研究七步 SOP，用於分析、研究、評估個股。美股或英文資料用英文版，台股用中文版。"
---

# Stock Analysis / 買股 SOP

Build a verifiable thesis for a stock from free public data. Not investment advice. / 用免費公開資訊建立可驗證的持股邏輯，非投資建議。

## When to use / 何時使用

- The user asks to analyze, research, or evaluate a stock.
- The user asks what to check before buying a stock.
- 使用者要分析、研究、評估某檔股票，或問買股前該看什麼。

## Which version to use / 該用哪一版

| Case / 情況 | Version / 版本 |
|-------------|----------------|
| US stock, or the materials are in English / 美股，或資料是英文 | **English version** |
| Taiwan stock / 台股 | **中文版 (Chinese version)** |

- Write the whole analysis in the language of the version you use. / 整份分析用所選版本的語言撰寫。
- If the two cases conflict (for example a Taiwan stock with English-only materials), ask the user which version to use. / 兩種情況衝突時（例如台股但只有英文資料），先問使用者要用哪一版。
- Never invent figures. If a number cannot be found, write "unavailable" (中文版寫「查無資料」) and state what you tried. / 不要編造數字，查不到就明說並寫出試過什麼。

## Output / 輸出

For each of the 7 steps, report: the data you found (with source and period), the computed ratio, the comparison with the prior quarter, and a one-line conclusion. End with the three answers from the final check.

七步每一步都要列出：查到的數據（附來源與期間）、計算結果、與上季比較、一句結論。最後回答「進場前的最後檢查」的三個問題。

---

# English Version (US stocks / English materials)

## Seven steps before buying a stock

### 1. Understand what the company sells

- From the latest earnings presentation, list revenue share by product / business.
- Separate high-margin growth businesses, cyclical businesses, and low-margin businesses.
- Track whether the revenue share of high-margin products rises quarter over quarter.

### 2. Look at core profitability, not just EPS

- From the consolidated income statement (SEC EDGAR 10-Q / 10-K), pull gross profit and revenue.
- Compute: `gross margin = gross profit ÷ revenue`.
- Compare with the prior quarter: rising means the core business is improving; several straight declines mean weaker pricing or a weaker cycle.

### 3. Verify that growth is actually happening

- Check capex and investment direction in the earnings presentation or material filings (8-K).
- Confirm the money goes into high-end, growing products / capacity.
- Cross-check with gross margin and high-end revenue share: expansion only counts as effective if spending rises **and** profitability improves.

### 4. Check inventory to catch a cycle turn early

- From the latest balance sheet and income statement, pull inventory and revenue.
- Compute: `inventory / revenue = inventory ÷ revenue`, and compare with the prior quarter.
- Healthy: the ratio falls while revenue rises. Watch for unsold-goods and price-cut risk when the ratio keeps rising while revenue stalls or falls.

### 5. Look for sustained institutional positioning, not one-day spikes

- Sum the net buying / selling of foreign investors and investment trusts over the last 5 trading days. (Taiwan-specific data. For US stocks use the closest public substitutes: 13F changes in institutional holdings, Form 4 insider trades.)
- Consistency over time, and different holders buying together, matter more than one big day.
- A one-day spike may just be short-term money or a next-day reversal trade.

### 6. Check the balance sheet for hidden bombs

- Pull goodwill and total assets. Compute: `goodwill / total assets = goodwill ÷ total assets`.
- When goodwill is high, assess the risk that weak acquisitions force impairments that eat into earnings.
- Do not read only the income statement; confirm asset quality too.

### 7. Look at price and technicals last

- Record the 3-year high, 3-year low, current price, and the position versus the 20-day / 60-day moving averages.
- Use price to judge whether you are at a rebound, a high, or a low. Do not use candlesticks to predict tomorrow.
- A rebound needs industry improvement and earnings growth behind it. At a low, first work out whether it is undervaluation or a fundamental turn to the downside.

### Final check before entering

If the price dropped 10% tomorrow, could I clearly state:

1. What does the company earn money from?
2. Is the current profit and growth backed by data?
3. What are the main risks, and what is my stop-loss / reason to stop holding?

If yes, consider building a position. If no, finish the fundamental research first.

---

# 中文版（台股）

## 買股票前的研究七步

### 1. 先搞懂公司賣什麼

- 從最新法說會簡報整理各產品／業務的營收比重。
- 分辨高毛利成長業務、週期型業務與低毛利業務。
- 追蹤高毛利產品的營收占比是否逐季上升。

### 2. 看本業獲利，不只看 EPS

- 從公開資訊觀測站抓「合併綜合損益表」的營業毛利與營業收入。
- 計算：`毛利率 = 營業毛利 ÷ 營業收入`。
- 與上季比較：上升代表本業改善；連續下滑代表價格或景氣轉弱。

### 3. 驗證成長是否真的發生

- 查法說簡報或重大訊息中的資本支出與投資方向。
- 確認資金是否投入高階、具成長性的產品／產能。
- 對照毛利率與高階產品營收比重：投入增加且獲利改善，才算擴產有效。

### 4. 檢查庫存，提早發現週期反轉

- 從最新資產負債表與損益表抓存貨、營收。
- 計算：`存貨占營收 = 存貨 ÷ 營收`，並與上季比較。
- 存貨比重下降且營收上升較健康；比重持續上升、營收停滯或下滑，留意滯銷與降價風險。

### 5. 看法人「連續布局」，不要追單日買超

- 統計近 5 個交易日外資與投信的買賣超累計。
- 連續性、不同法人同步買超，比單日爆買更有參考價值。
- 單日買超可能只是短線資金或隔日反手交易。

### 6. 查資產負債表的未爆彈

- 查商譽與總資產，計算：`商譽占總資產 = 商譽 ÷ 總資產`。
- 商譽偏高時，評估併購標的表現不佳造成減損、侵蝕獲利的風險。
- 不要只看獲利表，也要確認資產品質。

### 7. 最後才看價格與技術面

- 記錄近 3 年高點、低點、現價，以及 20 日／60 日均線位置。
- 用價格判斷自己處在反彈、高位或低位，不用 K 線預測明天漲跌。
- 反彈要有產業改善與獲利成長支撐；低位則先釐清是低估還是基本面轉空。

### 進場前的最後檢查

如果明天股價突然下跌 10%，我能否清楚說明：

1. 公司靠什麼賺錢？
2. 目前的獲利與成長是否有數據支持？
3. 主要風險與停損／不再持有的理由是什麼？

答得出來，再考慮布局；答不出來，先完成基本面研究。
