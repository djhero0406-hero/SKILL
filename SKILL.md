---
name: minimax-h3-director
description: Use for MiniMax H3 video prompt writing, MV/storyboard/CUT planning, T2VA I2VA FL2VA L2VA Ref2VA or supported Hybrid reference assignment, character emotion, POV, dialogue and lip-sync instructions, combat/camera/sound design, prompt checking and ComfyUI H3 workflow troubleshooting. 使用於 MiniMax H3 影片提示詞、分鏡、H03 Hybrid、P01 情緒演繹與相關除錯；不要用於無關任務。
---

# MiniMax H3 提示詞導演技能

本 Skill 是 **Codex 可調用的文字工作規範**。它不等於 MiniMax H3 模型、LoRA、ComfyUI 插件、影片生成 API 或聲畫同步驗收程式。

## 資料來源與讀取順序

1. 先讀 `references/MiniMax_H3_Prompt_Index.md`，找出用戶指定的技能 ID、範例調用與輸出形式。
2. 再按任務讀 `references/MiniMax_H3_Integrated_Library.md` 的必要章節；格式／素材角色看「格式協議」，演出看「導演與表演方法」，驗證、Relay 與診斷看「品質、Relay 與證據」。
3. 兩份參考文件來自用戶的整合稿，並非已重新核對的官方或現行工作流規格。保留來源內的適用範圍、例外與限制，不把歷史資料當成當前實測結果。

## 技能 ID 路由

- 格式及參考：H01 多模態格式、H02 首尾幀、H03 Hybrid。
- 導演敘事／動作：D01 Fisher 連續戰鬥、D02 土豆高密度攻防、D03 兔子電影槍戰、D04 寧版文武雙全、D05 關係與潛台詞、D06 情境與鋪墊回收、D07 贞贞 POV、D08 Jojocodex 武術。
- 表演與製作：P01 土豆情緒演繹、C01 戰鬥運鏡、A01 聲音設計。
- 檢查及工具：Q01 協議檢查、R01 Prompt Relay、W01 工作流診斷。

以上 H01、H03、P01 等是**技能庫內部的索引 ID**，不是 Codex 原生的 `$H03`、`$P01` 指令，也不是 ComfyUI 節點。Codex 的技能名稱是 `$minimax-h3-director`；在使用者提示中以「主要 H03、搭配 P01」選擇方法。

## 標準工作流程

1. 辨認工作類型：新提示詞、影片分鏡、局部 CUT 修改、完整專案腳本、協議檢查或 H3/ComfyUI 故障診斷。
2. 讀取用戶實際提供的圖片、影片、音訊、劇本及工作流文件。若無素材，不要假稱已看到；不要憑圖片數量自動決定首尾用途。
3. 依素材角色選 T2VA、I2VA、FL2VA、L2VA、Ref2VA。只有已提供適當首/尾幀，且下游確實支援時才選 T8 Hybrid。只提及「Hybrid」並不足以證明可啟用；欠缺資產時提供可行的原生模式或明標為規劃稿。
4. 選**一項主要導演技能**，視需要加入情緒 P01、運鏡 C01、聲音 A01 等，不把所有方法硬塞進成品。
5. 優先遵守用戶最新的硬性條件：角色與場景身份、起訖狀態、POV、人物站位、物件持有、單鏡／CUT 數、秒數、原句、說話人、禁配樂／聲音白名單、結局。只要求修改一個 CUT 時，交付該 CUT 的完整替代稿，其他 CUT 不改。
6. 按選定模式提供三欄或六欄 H3 提示詞。欄位名稱維持英文；依用戶要求使用中文相容或英文描述，對白與歌詞保留原語及原字。人聲按參考文件使用 `(S1)` 等 ASCII 聲源標記及 `<d>[Chinese] ...</d>` 等正確語言標籤，不擅自翻譯或添詞。
7. MV 對嘴任務：若有實際音訊，依可取得的聲音段落／歌詞時序寫唱歌與器樂間奏口部動作；沒有音訊或時間碼時，不要聲稱已精確對齊音節或驗證成片口型。用戶寫下的「精準」屬目標要求而非已完成結果。
8. 無配樂時使用 `non_diegetic_music: N/A`；若只允許指定音源，嚴守白名單，不能偷偷加呼吸、底噪、場音或音效。
9. 檢查輸出格式、參考編號、每句原文、秒數切點、角色行為、聲音層；區分「文本格式核對」、「語義核對」與「實際出片驗收」。
10. 輸出完整可複製稿。多 CUT 若要求一次複製，集中在單一程式碼區塊。僅在用戶要求時提供分鏡表、分析、譯稿或多版本。

## Codex 與工作流邊界

- 單純生成影片提示詞：只撰寫／輸出文本，不擅自修改工作站或專案檔。
- 用戶要求修改 ComfyUI 工作流、Prompt Writer、導演台程式時：先檢查**實際存在**的 repo、JSON、節點和日誌；修改前保持用戶現有工作流及備份，限定目標檔與可驗證範圍。此技能本身不提供 ComfyUI 控制或執行權限。
- 文字 Prompt Relay 事件稿不等於可執行 JSON；未提供真實下游 schema 時不得杜撰契約。
- 不宣稱已載入 LoRA、已完成聲畫同步、已渲染影片或已連線 ComfyUI，除非有工具操作與結果證據。

## 觸發範例

- `$minimax-h3-director 用 H03 搭配 P01，把圖1女主、圖2太空艙、圖3三花貓做成 10 秒 Ref2VA 提示詞；素材均作角色／場景參考，沒有首尾幀。`
- `$minimax-h3-director 用 D05 + P01 + A01 編排 8 秒人物對話，只保留原句和雨聲，不加配樂。`
- `$minimax-h3-director 用 Q01 只修正 CUT3 的聲源 ID 與時間切點，其他 CUT 完全不動。`
- `$minimax-h3-director 用 W01 分析這個 ComfyUI H3 JSON 和錯誤日誌，先找原因，不要直接改檔。`
