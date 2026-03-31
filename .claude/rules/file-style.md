# 檔案規範

## 基本格式
- 所有需求文件都是 Markdown 格式
- 檔案編碼都是 UTF-8
- 檔案內容以中文為主英文為輔

## 索引檔案（index.md）
- 格式為 Markdown 表格，標題列為 `| 編號 | 標題 |`
- 每筆記錄格式：`| A001 | 內部員工登入驗證 |`
- 依需求編號排序，新需求加在最後一列

## 輸入
- 需求文件放在 `input/` 資料夾，格式為 `*.md`
- 例如：`input/A001.md`
- 需求編號依序遞增（A001、A002、A003…），新需求自動沿用下一個編號

## 輸出
- 每份需求在 `output/` 下建立以需求編號命名的子資料夾
- 例如：`output/A001/`
- PlantUML 檔案輸出至該子資料夾，命名規則依據輸入檔名加上圖表類型後綴：

| 圖表類型 | 後綴 | 範例 |
|---|---|---|
| Use Case 圖 | -usecase.puml | output/A001/A001-usecase.puml |
| 活動圖 | -activity.puml | output/A001/A001-activity.puml |
| 序列圖 | -sequence.puml | output/A001/A001-sequence.puml |
| ER 圖 | -er.puml | output/A001/A001-er.puml |
