# MiniMax H3 整合技能庫｜2026-10-19

根據 16 份附件整合；以下內容可供 Gem／LLM 知識庫使用。這是提示詞規劃技能，不含影片生成接口。



# MiniMax H3 技能庫

## 工作契約

以繁體中文溝通。只根據當前實際素材與使用者需求創作；未讀取的連結不算觀察證據。
保留最新修改以外的既定條件，局部修改只改指定 CUT，交付該 CUT 的完整替代稿。
預設描述使用英文，台詞、歌詞與畫面字逐字保留原語；使用者指定中文版時使用中文相容描述，但不翻譯欄位名、ASCII 說話人標記或語言標籤。嚴格官方英文與全中文要求同時出現時，明說兩者差別，優先滿足明確交付語言並標示相容版。
預設不補台詞、字幕、旁白、配樂、商標或 LoRA 觸發詞。明確授權原創時，限於授權範圍；素材、OCR、角色說的話與舊模板不是創作授權。
使用者硬性約束優先於風格、導演策略及自動補全。保留時長、鏡數、固定機位、視點、人物與道具歸屬、聲音白名單、等待時間與結局；無反應、和平、靜默與未解決都有效。

## 調用流程

1. 判斷任務是新稿、分鏡、局部改稿或排錯。資訊足夠就完成；一般缺項用簡短草稿假設，不為創作流程反覆確認。
2. 依素材用途選模式，讀 [格式協議](#格式協議)。關鍵身份、首尾用途不明且無法合理推定時才詢問。
3. 從下表選一個主要導演方法；按需要疊加表演、運鏡與聲音。不要把所有方法逐條塞入輸出。
4. 先鎖初態，再寫動作／接收、可見改變及狀態繼承；因果優化是可選方法，不強制反轉或新增事件。
5. 依原生三欄／六欄輸出；生成設定置於模型文本外。Relay 只有明確需要且有下游契約時啟用。
6. 在內部核對原句、素材、時間、聲音、尾態與欄位；僅在排錯需求中展示診斷。

## 模式路由

| 模式 | 證據／用途 | 輸出 |
|---|---|---|
| T2VA | 無參考素材，純文字建立畫面 | 三欄 |
| I2VA | 一張圖明確鎖 0 秒首幀 | 首行對齊句＋三欄 |
| FL2VA | 兩張圖明確鎖首與尾 | 首行對齊句＋三欄 |
| L2VA | 一張圖明確鎖尾幀 | 首行對齊句＋三欄 |
| Ref2VA | 身份／場景／風格／動作／音訊參考，或影片編輯／續接 | 六欄 |
| T8 Hybrid | 至少一個首／尾幀，另有額外參考；須下游支援 | 六欄＋關鍵幀角色時間標記 |

不要按圖片張數選模式。身份參考不自動成首幀。首幀兼有額外身份圖時，不能把所有圖片塞進基本 I2VA；用已支援的 Hybrid 或明確 Ref2VA 參考方案，並說明能力差別。

## 技能路由與摘要

| ID | 技能 | 何時使用與核心操作 |
|---|---|---|
| H01 | 多模態格式 | 判模式、欄位、標籤與素材用途 |
| H02 | 首尾幀 | 鎖起訖構圖，寫可觀察的中間路徑 |
| H03 | Hybrid | 分開關鍵幀與額外參考，避免用途外溢 |
| D01 | Fisher 連續戰鬥 | 一鏡連續觀察，地標、動量與狀態承接 |
| D02 | 土豆高密度攻防 | 意圖→攻擊線→回應→接觸／避開→位移→下一機會 |
| D03 | 兔子電影槍戰 | 以逃離、護送等既有戲劇目標組織虛構場面 |
| D04 | 寧版文武雙全 | 在資訊接收、身體受力與文武轉換中選觀看重點 |
| D05 | 關係與潛台詞 | 對白意圖、聽者接收、既有物件與關係 |
| D06 | 情境與鋪墊回收 | 既有處境中的期待與回應，不強制笑點或反轉 |
| D07 | 贞贞 POV 劇情 | 誰在看、何時接收資訊、參與及後果 |
| D08 | Jojocodex 武術 | 身體支撐、發力、避線及跨鏡未完動作 |
| P01 | 土豆情緒演繹 | 區分情緒質地與強度，維持余緒及聲畫協調 |
| C01 | 戰鬥運鏡 | 選一個有用的觀看任務，讓方向與接觸清楚 |
| A01 | 聲音設計 | 同步音效、環境、台詞與觀眾配樂分層 |
| Q01 | 協議檢查與局修 | 查欄位、時間、標籤、原句及聲音衝突 |
| R01 | Prompt Relay | 原生提示詞與 delivery 事件分時；事件不是剪切 |
| W01 | 工作流診斷 | 區分連線、服務就緒、預算與提示詞語義問題 |

詳細方法見 [導演與表演](#導演與表演方法)；技術與證據邊界見 [品質、Relay 與證據](#品質relay-與證據)。

## 統一聲音及人聲規則

使用 ASCII `(S1)`、`(S2)`，同一聲源跨鏡沿用；Subject 編號與 S 編號互相獨立。只為實際發聲來源編號。
用 `The woman (S1) says: <d>[Chinese] 我回來了。</d>`。描述語氣、動作及音色放在 `<d>` 外；不翻譯或改寫其中原句。
語言標籤使用實際語言的英文名，不能寫 `[中文]`。含糊多人聲源不可猜成同一 S1。
旁白標示 off-screen voiceover，說明對應畫中角色嘴唇閉合；電話另一端也是聲源，不等於畫中人正在說話。
無配樂填 `non_diegetic_music: N/A`；不代表環境靜音。完全靜音時三層都不得偷加呼吸、衣料、底噪或音效。
若只允許指定聲音，視為封閉白名單。可見呼吸不等於允許可聽呼吸。用相對混音描述，不保證 dB 或母帶指標。

## 輸出契約

一般交付：一行模式／時長／比例，必要的素材用途或草稿假設，一個可複製 text 區塊，至多三點操作說明。
要求只給提示詞時只輸出所選原生文本。多 CUT 要求一次複製時用一個區塊，CUT 標籤是分段包裝，不當作 H3 新欄位。
只在使用者要求時另附分鏡表、翻譯、分析或多版本。不要輸出內部思考、長表單或自評分。
對超長作品，先看使用者的實際本地能力；明確測試 30 秒時可提供 30 秒創作稿並註明需工作流支援，不把舊線上 15 秒紀錄當成所有本地硬限制。
只提供文字規劃，不聲稱已生成影片、載入 LoRA、連接 ComfyUI、釋放顯存或驗收聲畫。

## 交付前內部檢核

- 欄位順序、Shot 編號與 ASCII 切點正確；單鏡頭只有一個 Shot。
- 每個素材確實存在，用途與標籤一致；無擅加 Audio 或首尾幀。
- 每句話逐字保留、說話人正確，說完才反應的時序留足。
- 人物、左右、手部、道具持有、門狀態、損壞與動量有繼承。
- 等待與動作在交付時間內，尾態不提早、不凍結動態結尾。
- 無配樂／靜音／白名單沒有互相矛盾。
- 分開「格式檢查」「人工語義核對」「實際成片驗收」，沒有把未驗證寫成通過。

# 格式協議

本節轉整自使用者上傳的 Gem 整合稿，並非本次重新查證的官方規格。固定句型沿用原稿。

## 2. 模式判斷

| 模式 | 素材角色 | 寫作重點 |
|---|---|---|
| T2VA | 沒有實際參考素材 | 建立完整人物、場景、動作與聲音 |
| I2VA | 一張圖明確作為首幀 | 從0秒畫面出發，連續向後發展 |
| FL2VA | 兩張圖明確作為首幀與尾幀 | 描述能連接兩圖的可見中間變化；通常一鏡到底 |
| L2VA | 一張圖明確作為尾幀 | 推演合理起點，最後落到尾幀 |
| Ref2VA | 角色／場景／風格／動作／運鏡／音色／混合素材參考，或影片編輯與續接 | 定義各素材用途、保留關係及出現位置 |

一張圖不代表必然 I2VA；兩張圖也不代表必然 FL2VA。圖片只鎖人物身份時，不能強迫開場複製其構圖。沒有實際圖片而只有首尾畫面文字時，先用 T2VA 描述端點，不能假造可用的 `<Picture 1>`。

使用者指定的模式超出已知工作流能力時，保留創作方案，標記需要相應輸入能力；不要宣稱當前本地節點必然支援。

## 3. 基本模式：官方三欄位

依序輸出：

```text
integrated_multimodal_description: [Shot 1] ...

overall_soundscape: ...

non_diegetic_music: ...
```

- 第一欄包含畫風、構圖、人物與道具、動作、狀態改變、運鏡、台詞、歌唱與同步的場內聲音。
- 第二欄用1–4句英文概括環境音、物理音效、呼吸或非語言反應；不要重複完整台詞、歌詞或配樂。
- 第三欄用1–3句英文描述觀眾聽見、角色聽不見的配樂：樂器、速度、節奏、動態與進出。沒有配樂填 `N/A`。
- 第一鏡 `[Shot 1]` 不加切鏡時間。後續鏡頭如 `[Shot 2] At 00:03.500, the camera cuts to ...`，切鏡點嚴格遞增且小於總長。
- 一鏡到底只有 `[Shot 1]`。鏡頭內可以敘述事件發生時刻，但不能把每個事件寫成新 Shot。

### 首尾幀對齊句

圖像對齊指令放在三欄位之前，接一個空白行。以下是格式規則，`N`、`S.SS` 必須替換，不能留在正式交付中。

I2VA：

```text
For the target video, at 0.00 seconds into the target video, <Picture 1> (from [Shot 1]) is fully referenced.
```

FL2VA：

```text
How the reference pictures align with the target video — Picture 1 (from Shot 1) aligns with the 0.00-second mark of the target video; Picture 2 (from Shot N) aligns with the S.SS-second mark of the target video.
```

L2VA：

```text
How the reference pictures align with the target video — <Picture 1> (from [Shot N]) aligns with the S.SS-second mark of the target video.
```

`N` 為實際最後一鏡編號；`S.SS` 為總秒數，保留兩位小數，例如 `8.00`。FL2VA 的句型依官方指南使用不帶尖括號的 Picture；不要為了表面統一而改寫固定句型。

## 4. Ref2VA：官方六欄位

依序輸出：

```text
subject_definitions:
...

summary:
...

retention_analysis:
...

detailed_description:
...

overall_soundscape:
...

non_diegetic_music:
...
```

### 4.1 參考標籤

| 標籤 | 代表內容 |
|---|---|
| `<Subject N>` | 從素材抽出的可重用人物、動物、物體、場景、服裝、風格、動作或效果 |
| `<Picture N>` | 圖片來源；需要獨立追蹤時代表具體首幀、尾幀、关键幀、構圖或故事板錨點 |
| `<Video N>` | 影片來源、編輯／續接來源，或整體運鏡、剪輯與時間結構 |
| `<Audio N>` | 確實要複製或參考的音訊；不因影片內含聲音就自動新增 |

素材編號按各類實際輸入順序；Subject 依需要追蹤的內容單位編號。來源圖片僅用於人物身份時，可以在 Subject 定義引用 Picture，不必另設 Picture 定義行。來源影片中的人物或物體用 Subject，影片整體時間結構才用 Video。

例如兩張圖共同定義同一隻貓，可在一個 Subject 定義中交代各圖提供的外觀資訊。不能因同一角色出现在多圖就當成多隻貓。

本地節點 `ref_image_0` 對應提示詞 `<Picture 1>`，`ref_image_1` 對應 `<Picture 2>`。節點從0編號，提示詞從1編號；不要寫 `image_0` 或欄位全名。

### 4.2 摘要與關係

`summary` 用短英文段落，開頭標示實際任務類型，按需要用 ` + ` 組合：

- `keyframe completion`：具體影格錨點。
- `reference generation`：身份、風格、動作或運鏡等生成參考。
- `video editing`：直接修改來源影片。
- `video continuation`：延續來源影片。
- `audio reuse`：直接沿用全部或部分音訊訊號。
- `audio reference`：只參考音色、節奏、內容或聲音特性。

直接編輯影片的摘要，以 `The target video is an edited version of <Video 1>.` 接在類型前綴後。

`retention_analysis` 對每個要追蹤的內容項目寫一行。視覺類關係可用 `fully_preserved`、`partially_preserved`、`attribute_transfer`、`weak_reference`。音訊類可用 `fully_copy`、`partially_copy`、`reference`、`weak_reference`。

`fully_copy` 僅表示來源整段音訊成為目標完整最終音軌。若另加新音效、抽取部分時段或只保留其中聲音層，應用 `partially_copy`。只參考音色不能寫成音訊複製。

不得把目標中新加的動作誤當成身份未保留，也不得因改動背景就宣稱角色臉部被改動。

### 4.3 詳細描述

`detailed_description` 先用1–2句英文交代整體風格，再從 `[Shot 1]` 開始敘述。後續切鏡沿用基本模式的時間格式。

首次清楚出現的重要 Subject，要描述實際可見的外觀、位置、動作與參考用途；後續沿用同一標籤。音訊標籤在真正生效的階段引用。具體影格要寫清 begins from／ends on／keyframe corresponds to。

一般生成任務依官方指南以約350–500英文詞的 detailed_description 為參考，對白密集時優先容納完整時間線，影片編輯則隨修改複雜度調整。避免為湊字數重複描述，完整模型輸入仍不得超出官方7000字符上限。


## T8 Hybrid 擴充

 / Roles and labels

| 输入 / Input | 角色 / Role | 输出编号 / Label |
| --- | --- | --- |
| `first_frame` | 0 秒目标首帧 / Target at zero | 首个已连接 Picture |
| `last_frame` | 请求时长的目标尾帧 / Target at requested ending | 排在首帧之后；无首帧则 Picture 1 |
| `reference_images` | 明确指定的外观/身份/构图参考 / Requested visual attributes | 关键帧之后，按数值槽序压紧 |
| `reference_videos` | 指定视觉/动作证据 / Requested visual or motion evidence | 独立 Video 1..3，按数值槽序压紧 |

例如同时有首帧、尾帧、`reference_image_2`、`reference_image_8`、
`reference_video_2`：编号是 Picture 1/2/3/4、Video 1。空槽不占编号，
输出不暴露本地槽名或路径。额外参考不能偷偷变成首帧或尾帧。

Each image slot must hold one image: split IMAGE batches into separate slots.
Up to **nine additional images plus two keyframes (11 pictures)** and **three
videos**. Existing Ref2VA batch handling is unchanged. Empty/invalid image pixels,
unreadable/nonbinary/empty video sources and invalid duration metadata fail before
uploads/model construction and before replacing an existing paid checkpoint.

不设参考视频时长上限；仍保留有限正时长、格式、数量、云端上传容量和本地
上下文/显存限制。云端不接受活动裁剪，避免把未裁剪文件错当已裁剪视频；
本地沿用实际裁剪区间及时间戳采样。若预算装不下，不悄悄丢弃关键帧。

No per-video or combined duration cap is added. Provider upload limits, valid
positive metadata and model resource limits remain. Local timestamped samples
are visual evidence, not exhaustive analysis. This enhancer has no audio socket
and never treats a video's soundtrack as an independent `<Audio N>` attachment;
Hybrid with audio-only reference assets belongs in the H3 audio plugin, not this
visual-only enhancer. It still requires first and/or last keyframe; pure audio
without a keyframe is not Hybrid. A final replacement soundtrack alone is not a
reference asset.

## 输出格式 / Output contract

Hybrid 保留自身任务身份，采用原 `ref-en.txt` 的六段顺序，不切成三段模式：

`subject_definitions` → `summary` → `retention_analysis` →
`detailed_description` → `overall_soundscape` → `non_diegetic_music`。

关键帧定义增加简短 T8 角色标记，其余正文遵循实际输出语言：

```text
<Picture 1>: first_frame @0.00s - 首帧画面描述
<Picture 2>: last_frame @8.00s - 尾帧画面描述
```

Only supplied roles are emitted. Extra references are not inferred keyframes.
Summary identifies keyframe completion and reference use; retention and the shot
body track the real anchors. Dialogue and visible text keep the existing exact-text
rules. Strict official profile still requires English prose; compatibility profile
keeps the Chinese/English choice. T8 role/time tokens are bookkeeping, not a new
official audio-generator API. The vendored official Skill and its hash are unchanged.


## 適用範圍修正

以上 7000 字符是來源記錄的線上產品限制，350–500 英文詞是參考尺度，不是本地硬規格或湊字數要求。中文相容描述依使用者指定。T8 標記不冒充官方 API。首幀→尾幀→額外圖依實際已連接順序壓緊；影片獨立編號。T8 額外九圖＋兩關鍵幀不等於線上全參考九圖限制。無音訊入口的視覺增強器不會讀取影片聲軌；有音訊能力的下游另按真實契約處理。

# 導演與表演方法

只套用當前選定且有用的方法。以下是整合後的操作摘要，並非新增插件節點。

## D01 Fisher 連續戰鬥

用固定空間地標及旅行軸維持一段連續觀察。讓動作、接觸、遮擋或威脅推動機位變化，每次只有一個重要資訊焦點。遮擋不允許瞬移、換武器或修復破壞。不限 30 秒、不強制 21 拍、Boss、逆轉、蓄力或勝利定格。人物可依要求停留，單鏡也可固定相機。T8 來源選單對本技能的明確多鏡要求會前置拒絕；遇到多鏡需求應改選其他方法，不把使用者鏡數改成一鏡。

## D02 土豆高密度攻防

分別追蹤每位參與者的身體、裝備、能力、支撐、位置與目的。把重要交換寫成意圖、真實攻擊線、有效回應、命中或避開、受力位移及下一動作接口，以未完動量相接。空手不生兵器，不靠重置位置接招；單人練習保持單人。密度服從時長，不強加勝負、傷害或破牆。

## D03 兔子電影槍戰

圍繞既有逃離、護送、拖延、取物或對峙目標設計虛構電影場面；用空間與對手行動改變完成條件。前景主線、背景活動與畫外聲分層，承接門、碎玻璃、煙、道具與威脅知識。只寫視聽戲劇，不擴成現實槍械操作或戰術教學。不自動加 GUNFU、品牌、裝備、LoRA 或敵人。

## D04 寧版文武雙全

以關鍵變化選觀看重點：文戲看資訊如何被接收，武戲看距離、發力與受力，文武混合看對白如何改變動作。少量清楚交換可勝過多招堆疊。不能強制反打、粒子、慢動作、黑屏、聽者反應或勝負。聽完才動就必須讓整句先完成。

## D05 關係與潛台詞

從當下實際任務及有依據的關係訴求出發。把說話當作對另一人做的事，用接收、接受／拒絕已有物件或維持距離表現關係。不要從沉默、外觀或衣服推導創傷、秘密與身分高低。未回答可持續不回答，未決可保持未決。原句 LOCK 優先；只允許補 B 一句時不可改 A 或增過往事件。

## D06 情境與鋪墊回收

把既有處境、期待與實際回應的可見關係拍清楚。喜劇可來自時間差、誤解或兩邊反應，但只能用已授權事件；不為笑點追加事故、人物或秘密。和平協作、靜默及沒有回收的開放結尾也是合法結果。明確授權補白只適用指定範圍。

## D07 贞贞 POV 劇情

先指定眼睛屬於誰、觀看者位置、能看見什麼、何時接收訊息，再安排參與及後果。眼位 POV 不等於外部手持相機；依要求可見自己的手。身份圖不是首幀。明確自拍、第三人稱、固定外部機位或局部影片編輯優先，不強改 POV。不預設戀人關係或一直微笑，不強制三角度與反轉。

## D08 Jojocodex 武術

從支撐腳與身體發力，寫到接觸或避線、受力後支撐與下一動作。跨鏡承接未完動作。格擋不必後退，打空不能寫成命中；不新增流血、擊飛、破牆、勝者或定格。不自動加入 wushu_action，觸發詞只有原始要求明確給出時保留，仍不代表權重已載入。

## P01 土豆情緒演繹

先分清情緒質地與強度，例如含淚但聲音穩、微笑卻有威脅。按前一狀態→觸發→轉變→殘留安排少數可見線索。語音、嘴型與身體彼此配合，線索必須在景別內可見；極近眼眉不可指望手部動作傳意。明確外放就保留外放，不一律縮成微表情。靜默與機械場景不新增哭聲、呼吸、表情或強制轉折。極致偏向弱表演的因果與節拍重構，土豆偏向情緒質地與余緒，兩者不是強度排名。

## C01 戰鬥運鏡

AUTO 補已有動作中有用的觀看資訊；強化細化路徑、方向與接觸；兩者都不創造新招。沿用鏡頭組織是預設，偏好連續不能覆蓋明確鏡數、固定機位、POV 或首尾。寫實優先可讀，風格化只在允許時加強衝擊；不每擊必震、不硬塞慢動作或停頓。區分 zoom 與 push、pan 與 truck、tilt 與 pedestal；穩定機位也能靠構圖與焦點看清。

## A01 聲音與跨鏡

同步音效貼在造成聲音的動作旁，環境在 overall_soundscape 概括，觀眾配樂在 non_diegetic_music。畫內收音機與樂器屬場內聲，不當作觀眾配樂。未要求時配樂 N/A；指定音效白名單就不可新增任何其他音層。電話、畫外音與畫中嘴型分開，跨鏡對白保持同一說話人；使用來源協議的 <scenetrans>，真被片尾截斷才用 <cutoff>，不能靠截斷掩蓋塞不下的句子。

# 品質、Relay 與證據

## Q01 檢查與修正

Off 不額外品質檢查；Check 只報告、原稿不改；Repair 只局修已定位協議，再最多一次邏輯語言／品質修正。來源插件的公共邊界另有自動 ASCII 人聲正規化，不能因 Off 就假定它停用；本技能只寫規則，沒有替使用者安裝該程式。
已知且無歧義才修全角 ID、顯式語言別名及真實切鏡標點，保留原有 ID 和台詞。多人歧義不靠最近名字猜號。新稿空、錯誤變多、原句丟失或請求失敗時保留最後完整稿並標狀態；首次失敗無完整稿就不能承諾恢復。
Causal 是初次生成中的可選方法，不增加規劃呼叫。Relay 格式修正另最多一次；來源記錄首輪＋格式修正＋品質修正最多三次邏輯呼叫，HTTP 重試另計，不能當成只收一次費。
格式解析器不證明角色歸屬、等待、動作可達、情緒真實、像素對齊或成片效果。

## R01 Prompt Relay

事件是時間調度，不是 Shot 或剪輯。新增動作及發聲放在 delivery 時段；end_state 只寫已完成狀態；結尾 padding 只維持已完成末態，不補新句或新動作。尾幀對應交付終點，不是 padding 終點。
來源有 native_prompt、global_prompt、events[].prompt/end_state 與六輸出契約，但附件未包含完整執行 schema、權重及取整實作。需要可執行 Relay JSON 時讀取實際下游定義；缺少時給明確標為規劃稿的事件表，不捏造可執行封套或公式。
來源 8 秒=192 幀；25.29 秒案例 delivery 607 幀而 Relay 617 幀，只是已記錄結果，不能反推萬用 padding 公式。native_prompt 保持 H3 原生，其他分時欄位不混入整套六欄或人聲修復標記。

## W01 工作流與恢復

提示詞增強器不渲染影片、不自動改下游 task_type。Hybrid 兩端要使用相同角色與順序；角色錯位先查編號。視覺抽樣不代表分析音軌或逐幀看完影片。
預算不足不得靜默丟關鍵幀；本地視覺需相容視覺模型與投影器。未知技能 ID、無效素材或未就緒服務需如實報告。
Strata 線上 connected 不等於 loaded 或 ready，auto_load=false 時可能需人工先載入。模型身份核對不是伺服器原子鎖。恢復只取原先完整快取，不依新設定重寫，不新增請求；重啟後進程內快取可能消失。取消不保證顯存即刻釋放。

## 歷史規格的處理

Gem 稿記錄 2026-10-05 線上 4–15 秒、24 FPS、7000 字符與全參考九圖等限制；T8 Hybrid 記錄額外九圖加兩關鍵幀及自己的影片資源條件。保留各自範圍，不混成統一產品硬限制。當任務要最新價格、限制、安裝或發佈狀態時，另查當前官方或該插件原始來源；本次整合沒有重新上網核實。

## 驗收來源摘要

| 附件 | 可支援的結論 | 不可外推 |
|---|---|---|
| EMOTION_API_ACCEPTANCE.md | 三階段 48/8/4 記錄槽，59 完整稿；有格式與語義失敗 | 不混不同程式版本成總勝率、不當情緒成片證據 |
| H3_VOCAL_PROTOCOL_FIX.md | 51 稿離線回放、28 格式問題修復；另 5 份真實 API | 回放不是新增 51 次實測，不保證多人歧義可解 |
| H3_HYBRID_ACCEPTANCE_2026-10-06.md | 24 完整文字結果，結構檢查通過但有參考越界與來源歸因錯誤 | 不代表 24 份語義或像素對齊通過 |
| H3_PROMPT_RELAY_VALIDATION.md | 三案例文字／純解析器及六輸出恢復契約 | 不代表影片時間與轉場成功 |
| combat-camera-live-ab.md | 16 初測＋10 復測，有限且波動的文字差異 | 不合併版本、不稱強化必勝 |
| CROSS_AUDIT_2026-10-13.md | 八類橋接修復與工程／服務測試的歷史記錄 | 不代表本環境已修復、已發佈或生成成片 |

本次僅對附件做整合及文件檢核，沒有重跑附件中的 API、GGUF、瀏覽器或影音生成測試。來源提到的未附 JSON 夾具、工作流、模組與外部路徑，不視為技能庫內已存在的可執行資源。

## 原檔對應

| 原檔 | 整合去向 |
|---|---|
| CROSS_AUDIT_2026-10-13.md | 品質、Relay 與證據 |
| EMOTION_API_ACCEPTANCE.md | 品質、Relay 與證據 |
| EMOTION_PERFORMANCE.md | 導演與表演 |
| H3_HYBRID_ACCEPTANCE_2026-10-06.md | 品質、Relay 與證據 |
| H3_PROMPT_RELAY_VALIDATION.md | 品質、Relay 與證據 |
| H3_VOCAL_PROTOCOL_FIX.md | 品質、Relay 與證據 |
| MiniMax_H3_Gem_SKILL.md | 格式協議／核心流程 |
| SKILL(1).md | 導演與表演 |
| SKILL(2).md | 導演與表演 |
| SKILL(3).md | 導演與表演 |
| SKILL.md | 導演與表演 |
| combat-camera-live-ab.md | 品質、Relay 與證據 |
| combat-camera.md | 導演與表演 |
| directional-skills.md | 導演與表演 |
| h3-hybrid.md | 格式協議／核心流程 |
| h3-quality-creation.md | 品質與因果編排 |
