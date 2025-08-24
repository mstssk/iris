# Naming
- Iris（ギリシャ神話の虹の女神 → 多方向に繋ぐイメージ）

# 実装方針
- 入力の動線は2つ
  - Cmd+I → ポップアップ&入力欄に初期フォーカスして、質問を入力できるようにする
  - Omniboxにkeyword入力 → 質問を入力できるようにする
- バックグラウンドでメッセージを受け取って、各生成AIチャットのタブを開いて入力させる
- TODO タブを開いてcontent-scriptsで入力させる流れの検証

## 入力欄にテキスト入力する技術的検証

ProseMirrorやQuillを使用しているため、通常のinputやtextareaに対してのvalue操作ではなく、以下のような方法でテキストを挿入する必要がある。

1. contentEditableな要素にfocus()
2. document.execCommand("insertText", false, "入力したいテキスト");
3. elem.dispatchEvent(new KeyboardEvent("keydown", { key: "Enter", code: "Enter", keyCode: 13, which: 13, bubbles: true, cancelable: true }));

※ execCommandは非推奨だが、Quillでも動く良い方法を見つけられなかった。InputEventのdispatchEventで可能なら実装したい。

# References
- chrome.commands  |  API  |  Chrome for Developers https://developer.chrome.com/docs/extensions/reference/api/commands?hl=ja
- chrome.omnibox  |  API  |  Chrome for Developers https://developer.chrome.com/docs/extensions/reference/api/omnibox?hl=ja
