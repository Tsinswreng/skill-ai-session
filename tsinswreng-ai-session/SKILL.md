---

name: tsinswreng-ai-session

description: 把每輪AI對話自動保存到文件上。僅在需要時閱讀此skill。

---

## 未使用此skill時的情況

- 用戶: 輸入提示詞
- AI:
  - 思考
  - 工具調用(可能)
  - 最終輸出答復

{最終輸出答復}是此輪對話中, AI對用戶的{輸入提示詞}的最終答復。 一般都是markdown 但問答歷史是顯示在AI Agent上的, 不會自動寫入文件裏。

## 此skill目的

把AI的{最終輸出答復}以typst格式整理到文件裏。

## 文件格式

```typ
#import "@local/tsinswreng-scriptorium:0.1.0": *
#show: _Show
#import AiSesn: *
#let T = Round

#let Terms = MkTerms(T=>
	T[-<Name>][Descr]
)
#H[Terms][
	#RenderTerms(Terms)
]

#T[2026_1117_115623][
	//此區域供用戶編寫提示詞
][
	//此區域供AI編寫最終答復
]
```

## 你需要做的

用戶會給你指定會話文件的路徑。 讀此文件 直接從最後的部分開始讀, 找到此文件中**最後一個**`#T[]`塊, 格式是`#T[時間][用戶提示詞][AI最終答復]`。 讀取用戶提示詞, 根據用戶提示詞來行動。 當行動結束後, 你準備輸出最終答復時, 把最終答復 以 typst 語法 **重定向**到 AI最終答復 的位置。

這個操作類似**重定向**, 即把你原來的輸出 **重定向** 進文件裏 而不是複製 即 **寫進文件之後就不要再重複輸出最終答復**

## 注意事項

- 只看最後一個`#T`塊
- 只把你的最終答復寫到最後一個`#T`塊的對應位置, 未經許可 禁止修改文件的其他部分
- 必須輸出typst格式, 不要包在代碼塊中。禁止用markdown
- 按 typst skill的規範寫! 必須看typst skill
- 寫進文件之後就不要再重複輸出markdown的最終答復
