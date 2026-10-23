# B 組員交付包（題庫與評估）v1.0 — 2026-10-23

## 檔案

| 檔案 | 給誰 | 用途 |
|---|---|---|
| `question_bank_zh-TW_v1.0.xlsx` | A、C、B | 主檔：questions / pairs / topics / scoring_template / metrics / qc_checklist / changelog |
| `question_bank_zh-TW_v1.0.csv` | C | 同 questions 表，UTF-8（BOM） |
| `question_bank_zh-TW_v1.0.jsonl` | C | 同內容，expected_points 與 sources 為結構化陣列，供程式讀取 |
| `prompts_only_zh-TW_v1.0.csv` | C、A | 只含送入模型的七欄；**測試程式只讀這個檔，避免評分依據混入模型輸入** |
| `scoring_codebook_v1.0.md` | 三人 | 題庫原則、欄位、評分規則、指標、流程、交接標準、AI 初評提示模板 |

## 給 A（現在就能用）

- 用 `prompts_only_zh-TW_v1.0.csv` 中 `split = dev` 的 20 題（P001–P010、N001–N010）跑環境與 Heretic 候選版本。
- **test 題（P011–P030、N011–N030）不得用於挑選或調整 Heretic 版本。**
- 請回傳：Heretic 所用資料集名稱／版本／切分／樣本數（或「無法確認」），我會比對是否與 test 題重疊並記錄。

## 給 C

- 題庫版本號 `1.0`；主題清單見 `topics` 表；評分表欄位見 `scoring_template` 表（前 5 欄由你產生，含 `status`）。
- 測試條件：兩版同 system prompt、同 chat template、temperature 0 或固定 seed、max_tokens ≥ 1,024；40 題 × 2 版 = 80 筆正式嘗試，dev 題另跑 40 筆供校準。
- 回傳時附 `response_map.csv`（response_id ↔ run_id, model_variant），評分期間我不看。
- 每筆回答保存欄位：run_id, question_id, model_variant, model_revision, prompt_version(=bank 1.0), system_prompt, generation_config, seed, response, latency, output_tokens, finish_reason, status, error_message。

## 下一步（B）

1. 收到 dev 40 筆回答 → 三人試評 → 修訂 codebook（→ v1.1）。
2. 收到正式 80 筆 → AI 初評 → 人工初評 → 25% 複核 → 共識 → 一致率／κ。
3. 第二輪：zh-CN、en 版本（同 ID），反向翻譯確認後加入。
