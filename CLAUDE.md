# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# 專案說明

這是公司內部訂便當系統的 UML 文件產生規範。

## 技術
PlantUML

## 系統架構
- 前後端分離系統
- 身份驗證採用 JWT（JSON Web Token），不使用 Session

## 限制
- UML 圖的標籤、說明文字一律使用繁體中文
- 每個需求檔案需產出 4 種圖，缺一不可
- 不要自行補充需求文件沒有提到的功能
- API 路徑依需求文件中定義的為準，不自行命名

## 輸入
- 需求文件放在 input/ 資料夾，格式為 *.md
- 例如：input/A001.md
- 需求編號依序遞增（A001、A002、A003…），新需求自動沿用下一個編號

## 輸出
- 每份需求在 output/ 下建立以需求編號命名的子資料夾
- 例如：output/A001/
- PlantUML 檔案輸出至該子資料夾，命名規則依據輸入檔名加上圖表類型後綴：

| 圖表類型 | 後綴 | 範例 |
|---|---|---|
| Use Case 圖 | -usecase.puml | output/A001/A001-usecase.puml |
| 活動圖 | -activity.puml | output/A001/A001-activity.puml |
| 序列圖 | -sequence.puml | output/A001/A001-sequence.puml |
| ER 圖 | -er.puml | output/A001/A001-er.puml |

## 各圖職責
- **Use Case**：列出所有使用者角色與其可執行的功能
- **活動圖**：描述主要流程的步驟、判斷與分支
- **序列圖**：描述使用者、系統、資料庫之間的互動順序
- **ER 圖**：描述資料表的欄位與關聯（含 PK/FK 標注）

## 索引
- 專案根目錄維護一份 `index.md`，記錄所有需求的編號與標題
- 格式：`A001 : 內部員工登入驗證`
- 每次新增需求文件時，同步更新 `index.md`

## 執行方式
當我說「處理 A001」時，你需要：
1. 讀取 input/A001.md
2. 建立 output/A001/ 資料夾
3. 依序產出 4 個 .puml 檔案到 output/A001/
4. 更新 index.md 加入該需求的編號與標題（若尚未存在）
5. 完成後列出產出的檔案清單確認
