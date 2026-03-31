---
name: sync-openapi
description: 更新根目錄的 openapi.yaml，同步所有需求的 API 定義。當新增或修改需求後需要同步 openapi.yaml 時使用。
---

## 執行策略

**更新現有檔案，不重新產出。**
`openapi.yaml` 包含完整的 `components/schemas` 與 `components/responses`，直接覆蓋會遺失已維護的 Schema 定義。正確做法是：
- 有新增 API → 在 `paths` 區段新增對應路徑
- 有新增資料欄位 → 在 `components/schemas` 新增或更新對應 Schema
- 有修改 API → 更新對應路徑的內容
- 有刪除 API → 移除對應路徑

## 執行步驟

1. 讀取 `index.md`，取得所有需求編號與標題
2. 依序讀取每個需求的 `input/{編號}.md`，擷取 `## API 路徑` 區段
3. 對照現有 `openapi.yaml` 的 `paths`，找出新增、修改、刪除的 API
4. 更新 `openapi.yaml`：
   - 新增或修改 `paths` 中對應的路徑定義
   - 若有新資料結構，在 `components/schemas` 新增對應 Schema
5. 若需求文件中無 `## API 路徑` 區段（如 A003、A009），該需求跳過

## 格式規範

### Tags
每個 API 的 tag 格式為 `{編號} {功能群組名稱}`：
```yaml
tags: [A001 員工登入]
tags: [A001 管理員帳號]
tags: [A002 員工訂餐]
tags: [A006 管理員訂單]
```

### Schema 引用
requestBody 與 response 的資料結構統一用 `$ref` 指向 `components/schemas`，不直接寫 `type: object`：
```yaml
requestBody:
  required: true
  content:
    application/json:
      schema:
        $ref: '#/components/schemas/LoginRequest'
responses:
  '200':
    content:
      application/json:
        schema:
          allOf:
            - $ref: '#/components/schemas/ApiSuccess'
            - type: object
              properties:
                data:
                  $ref: '#/components/schemas/LoginData'
```

### 共用 Response 引用
標準錯誤回應統一用 `$ref` 指向 `components/responses`：
```yaml
'400':
  $ref: '#/components/responses/BadRequest'
'401':
  $ref: '#/components/responses/Unauthorized'
'403':
  $ref: '#/components/responses/Forbidden'
'404':
  $ref: '#/components/responses/NotFound'
'409':
  $ref: '#/components/responses/Conflict'
```

### Security
- 公開 API（登入、忘記密碼、Refresh Token）加上 `security: []` 覆蓋全域設定
- 需要驗證的 API 不需另外寫 security（全域已設定 bearerAuth）

### 路徑參數
路徑中的 `{id}` 等參數統一在 `parameters` 中定義：
```yaml
parameters:
  - name: id
    in: path
    required: true
    schema:
      type: integer
```
