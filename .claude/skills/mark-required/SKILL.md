---
name: mark-required
description: 標示 ER 圖與 OpenAPI Schema 中的必填欄位。當需要標記欄位必填狀態時使用，例如「標示 A001 必填欄位」。
---

## 使用方式

指定單一需求：
```
mark-required A001
```

同時指定多個需求：
```
mark-required A001 A002
```

不指定編號則處理所有需求：
```
mark-required
```

## 執行步驟

1. 讀取指定需求的 `output/{編號}/{編號}-er.puml`
2. 更新 ER 圖：在所有 NOT NULL 欄位名稱前加上 `*`，可為 NULL 的欄位不加（並加上「可為 NULL」備註）
3. 對照 `openapi.yaml`，找出對應的 Entity Schema（回應用的資料結構）
4. 更新 OpenAPI：在 Entity Schema 新增 `required` 陣列，列出所有必填欄位；nullable 欄位加上 `nullable: true`

## 欄位判斷原則

### ER 圖（PlantUML）

| 標記 | 意義 |
|---|---|
| `* 欄位名` | NOT NULL（必填） |
| `欄位名` | 可為 NULL（選填） |

常見 NOT NULL 欄位：PK、FK（除非明確為 optional）、name、status、created_at、updated_at、is_active、is_admin
常見 nullable 欄位：description、error_message、triggered_by（手動觸發者）、sent_at、department_id（員工尚未分配部門時）

### OpenAPI Schema

- **Request Schema**（CreateXxxRequest、UpdateXxxRequest）：依需求文件定義，通常已有 `required`
- **Entity Schema**（Employee、Supplier、Menu、Order 等回應用結構）：依 ER 圖 `*` 欄位對應加入 `required` 陣列；nullable 欄位加 `nullable: true`

## 注意

- 規格書（input/*.md）**不需要**標示必填欄位，以 ER 圖與 openapi.yaml 為準
- PK 欄位（`<<PK>>`）永遠是 NOT NULL，在 ER 圖用 `* id : INT <<PK>>` 表示
- A005 的 `triggered_by`、`sent_at`、`error_message` 為 nullable，保持無 `*` 標記
