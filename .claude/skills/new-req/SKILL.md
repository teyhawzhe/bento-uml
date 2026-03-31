---
name: new-req
description: 處理新需求建檔，讀取 input/{編號}.md 產出 4 種 UML 圖並同步 index.md、usecase.puml、openapi.yaml。當使用者指定編號要產出 UML 且 input/ 已有對應需求文件時使用，例如「處理 A014」、「產出 A014 的圖」。若需求文件尚未建立，請先用 gather-requirement。
---

## 執行步驟

1. 讀取 `input/{編號}.md`，理解需求內容
2. 建立 `output/{編號}/` 資料夾（若尚未存在）
3. 依序產出 4 個 `.puml` 檔案到 `output/{編號}/`：

| 檔案 | 職責 |
|---|---|
| `output/{編號}/{編號}-usecase.puml` | 列出所有角色與可執行的功能 |
| `output/{編號}/{編號}-activity.puml` | 描述主要流程的步驟、判斷與分支 |
| `output/{編號}/{編號}-sequence.puml` | 描述使用者、系統、資料庫之間的互動順序 |
| `output/{編號}/{編號}-er.puml` | 描述資料表的欄位與關聯（含 PK/FK） |

4. 更新 `index.md`，加入該需求的編號與標題（若尚未存在）
5. 同步根目錄的 `usecase.puml`（執行 sync-usecase 邏輯）
6. 同步根目錄的 `openapi.yaml`（執行 sync-openapi 邏輯）
7. 標示必填欄位（執行 mark-required 邏輯）
8. 列出產出的檔案清單確認

## 產出原則

- 所有標籤、說明文字一律使用繁體中文
- API 路徑依需求文件定義為準，不自行命名
- 不補充需求文件沒有提到的功能
- 若需求文件尚未放入 `input/`，請先建立需求文件再執行此指令

## 注意

- 此指令用於**全新需求**的初次建檔
- 若需求已有 UML 圖需要更新，請使用 update-uml
