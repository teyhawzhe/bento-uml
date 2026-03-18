## 目標
讀取 output/ 資料夾內的需求文件，依照規範產出 4 種 PlantUML 檔案到 input/ 資料夾。

## 觸發方式
當使用者說「產出 UML」或「處理 {編號}」時執行此流程。

## 互動流程

### Step 1：確認目標文件
詢問使用者：
「請問要處理哪個需求編號？（例如：A001）
 或是輸入「全部」來處理 output/ 內所有尚未產出的需求。」

### Step 2：讀取需求文件
讀取 output/{編號}.md，若檔案不存在則告知：
「找不到 output/{編號}.md，請先執行需求收集流程。」

### Step 3：確認產出範圍
顯示即將產出的檔案清單，請使用者確認：
「即將為 {編號} 產出以下 4 個檔案：
 - input/{編號}-usecase.puml
 - input/{編號}-activity.puml
 - input/{編號}-sequence.puml
 - input/{編號}-er.puml
 確認開始產出？」

### Step 4：依序產出 4 種圖

#### Use Case 圖（-usecase.puml）
- 列出需求文件中所有使用者角色
- 每個角色對應其可執行的功能
- 標注系統邊界

#### 活動圖（-activity.puml）
- 依照需求文件的「主要流程」步驟繪製
- 包含「例外情況」的判斷分支
- 起點與終點需標示

#### 序列圖（-sequence.puml）
- 參與者：使用者角色、系統、資料庫
- 依照主要流程描述互動順序
- 例外情況用 alt/else 區塊表示

#### ER 圖（-er.puml）
- 依照「資料欄位」建立 Entity
- 自動推斷合理的欄位型態
- 標注 PK、FK 與 Entity 之間的關聯

### Step 5：完成通知
「已完成產出，共 4 個檔案：
 ✓ input/{編號}-usecase.puml
 ✓ input/{編號}-activity.puml
 ✓ input/{編號}-sequence.puml
 ✓ input/{編號}-er.puml

 需要繼續處理其他需求，還是收集新需求？」

## 注意事項
- 所有 PlantUML 標籤、說明文字一律繁體中文
- 不要自行補充需求文件沒有提到的功能或欄位
- 若需求內容不足以產出某種圖，告知使用者缺少哪些資訊
- 產出前確認步驟不可跳過
```

---

## 兩個 SKILL 的分工
```
gather-requirement.md
  → 互動問答 → 寫入 output/*.md

generate-uml.md
  → 讀取 output/*.md → 產出 input/*.puml