# 影片專題頁面（Prompt 摘要）

## 概覽
建立單一 HTML 檔案（包含 HTML/CSS/JS），展示一個以影片為主題的長篇故事頁面，包含 Landing、Onboarding（導覽卡）、以及四個章節（每章 200vh）。使用深色主題、響應式設計與流暢過渡（ease）。

---

## 資產（影片 URL）
1. 共用影片（Landing & Chapter 1 卡片）
   - https://d21rhj7n383afu.cloudfront.net/..._2000.mp4
2. 卡片 / 章節 2 影片
   - https://d21rhj7n383afu.cloudfront.net/..._2000.mp4
3. 卡片 / 章節 3 影片
   - https://d21rhj7n383afu.cloudfront.net/..._2000.mp4
4. 卡片 / 章節 4 影片
   - https://d21rhj7n383afu.cloudfront.net/..._2000.mp4

(完整 URLs 已由原始 Prompt 提供)

---

## 第一部分：Landing Page
- 高度：100vh
- 背景影片：自動播放、循環、靜音、playsinline、object-fit: cover（填滿）
- 中央文字：大標「探索未知的旅程」、副標「透過影像,發現世界的每個角落」
- 文字加深色陰影以提高可讀性
- 底部向下箭頭圖示：持續上下浮動動畫
- 點擊箭頭：平滑滾動到 Onboarding 區塊

---

## 第二部分：Onboarding（導覽卡）
- 高度：100vh，背景色 #0a0a0a
- 標題：「探索四個章節」置中
- 2x2 卡片網格（桌面/平板），手機改為一列
- 每張卡片包含：
  - 影片縮圖（video element，width:100%，height:300px，muted, playsinline）
  - 章節編號（CHAPTER 01~04，藍色 #4a9eff）
  - 標題與描述
- 卡片互動：
  - hover：卡片放大 1.05、陰影加深
  - hover：縮圖影片自動播放（靜音）
  - mouseleave：暫停並回到開頭
  - click：平滑滾動到對應章節（scrollIntoView, behavior: 'smooth'）

---

## 第三〜六部分：章節（CHAPTER 01〜04）
- 每章高度：200vh
- 背景影片層：
  - position: fixed，覆蓋全螢幕，object-fit: cover
  - muted, loop, playsinline，z-index:-1
  - 初始 opacity: 0；滾動到該章節時變為 1 並播放；其他章節影片變 0 並暫停
- 內容層：
  - 章節標題 sticky 固定於視窗上方 15vh（包含小標 CHAPTER 0X，藍色；大標 3.5rem）
  - 三個文字區塊垂直排列，間距 60vh
  - 文字區塊樣式：max-width 800px、置中、padding 40px、背景 rgba(0,0,0,0.75)、border-radius 8px、字體 1.3rem、line-height 1.8
  - 進場動畫：初始 opacity 0、translateY(50px)，進入視窗時切換到 opacity 1、translateY(0)，過渡 0.8s ease

- 每章具體文字內容按 Prompt 指定（章節標題與三段文字）

---

## JavaScript 功能（要求）
1. 使用 Intersection Observer 監測：
   - 章節標題（sticky）與各文字區塊：進入視窗時加上 `visible` class（觸發 CSS 過渡）
   - 章節整體：當某章節進入（threshold 合理設定）時切換背景影片的 opacity 並播放/暫停其他影片
2. 卡片行為：
   - hover / touchstart：縮圖影片播放（靜音）
   - mouseleave / touchend：影片暫停並回到 0（currentTime = 0）
   - click：scrollIntoView({ behavior: 'smooth' }) 到對應章節
3. 箭頭點擊：平滑滾動到 onboarding
4. 不使用 localStorage/sessionStorage
5. 所有影片加上 playsinline 屬性以提升手機相容性

---

## 響應式（重要）
- 手機（max-width: 768px）
  - 卡片改為單欄
  - 標題字體縮小（hero 與章節大標）
- 平板/桌面：卡片維持 2x2

---

## 其他注意事項
- 深色主題為主（背景 #0a0a0a 等）
- 所有過渡使用 ease 緩動
- 可考慮在使用者離開頂部時暫停 hero 影片以節省資