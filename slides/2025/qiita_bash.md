---
marp: true
theme: ../../themes/3shake-theme.css
paginate: true
math: mathjax
mermaid: true
style: |
  :root {
    --logo-url: url("../../assets/images/3shake-cover.png");
    --mini-font-size: 20px;
    --header-footer-height: 50px;
    --black: #333;
  }
  /* Add highlight-red class */
  .highlight-red {
    color: rgb(224, 64, 64);
  }
  /* 通常ページの左下にロゴを表示（より左下に押し込む） */
  section:not(.title)::before {
    content: "";
    position: absolute;
    left: 15px;  /* より左に */
    bottom: 15px;  /* より下に */
    width: 60px !important;  /* ロゴサイズを調整 */
    height: 60px !important;  /* ロゴサイズを調整 */
    background-image: var(--logo-url);
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
    opacity: 0.9;
    z-index: 100;
  }
  /* 背景色付きスライドではロゴ色を反転 */
  section[data-background-color="dark"]::before {
    filter: brightness(0) invert(1);
  }
  /* タイトルページのページ番号を非表示 */
  section.title::after {
    display: none;
  }
  /* タイトルスライドのロゴスタイル */
  .title-logo {
    position: fixed;
    top: 5px;
    left: 5px;
    width: 240px !important;
    height: auto;
    z-index: 9999;
  }
  /* すべての画像サイズを上書き - 3shake-logo.pngのみに適用 */
  img[src*="3shake-logo.png"] {
    max-width: 240px !important;
    width: 240px !important;
  }
  /* タイトルとサブタイトルのサイズ調整 */
  .title h1 {
    font-size: 2.2em !important;
  }
  .title h1 span {
    font-size: 0.75em !important;
    display: inline-block;
    line-height: 1.3 !important;
  }
  .title h3 {
    font-size: 1.1em !important;
    margin-top: 0.1em !important;
  }
  /* 作者情報のスタイル */
  .author-info {
    position: absolute !important;
    bottom: 40px !important;
    left: 100px !important;
    padding-left: 0 !important;
    text-indent: 0 !important;
    font-size: 0.9em !important;
    color: white !important;
    font-weight: bold !important;
  }
  /* スライドタイトル（h2）のスタイル */
  section h2 {
    font-size: 1.5em !important;
    margin-top: -25px !important;
    padding-top: 0 !important;
    margin-bottom: 10px !important;
    color: black !important;
    border-bottom: 1px solid #dadce0 !important;
  }
  /* コンテンツエリアの上部マージンを調整 */
  section > *:not(h2):not(header):not(footer) {
    margin-top: 1.2em !important;
  }
  /* 引用（参考文献）のスタイル */
  blockquote {
    border-top: 0.1em dashed var(--black);
    font-size: var(--mini-font-size);
    width: 100%;
    position: absolute;
    bottom: var(--header-footer-height);
    left: 0;
    padding: 10px 20px;
    margin: 0;
    box-sizing: border-box;
  }
  /* カスタムテーマにMermaidのスタイル設定を追加 */
  mermaid {
    display: block;
    margin: 0 auto;
  }
  /* 参考文献用のスタイル */
  .reference-right {
    font-size: 0.4em;
    text-align: right;
    margin-right: 20px;
    margin-top: -15px;
    display: block;
    width: 30%;
    margin-left: 70%;
  }
  /* 小さい文字用のスタイル */
  .small-text {
    font-size: 0.95em !important;
    line-height: 1.3 !important;
  }
  .small-text ul li {
    font-size: 0.95em !important;
    line-height: 1.3 !important;
    margin-bottom: 0.4em !important;
  }
  .small-text ul ul li {
    font-size: 0.95em !important;
    line-height: 1.3 !important;
    margin-bottom: 0.3em !important;
  }
---

<!-- 
_backgroundColor: #0a1929
_color: white
_class: title dark
-->

![bg](../../assets/images/3shake-background-full.png)

<img src="../../assets/images/3shake-logo.png" alt="3-SHAKE logo" style="position: fixed !important; top: 30px !important; left: 100px !important; width: 240px !important; height: auto !important; z-index: 9999 !important;">

<div class="title" style="text-align: left; margin-top: 100px; margin-left: 20px; padding-left: 0; max-width: 70%;">

# <span style="font-size: 1.0em !important; line-height: 1.4 !important; display: inline-block;">AIコードエディタは開発を変えるか？</br>Cursorをチームに導入して1ヶ月経った本音</span>

</div>

<div class="author-info" style="text-align: left; padding-left: 0; text-indent: 0;">
2025/5/28 Qiita Bash 最近ハマっている生成AI活用法を語ろう！</br>太田 暢(@iorandd)
</div>

---

<!-- _backgroundColor: white -->

![bg left:25% w:70%](../../assets/images/iorandd_icon.jpg)
## 太田 暢([@iorandd](https://x.com/iorandd))

<div class="info-box">
株式会社スリーシェイク</br>
SRE伴走型コンサルティングサービス「Sreake」事業部</br>
アプリケーション開発支援チーム エンジニア
</div>

<p style="margin-top: 30px !important;">阪神ファン、エニタイムで筋トレ始めて3ヶ月</p>

---

## 本日のスコープ

### 📣 話すこと
- クライアントワークにおける事例
- AIエディタ導入の実体験とチームの適応プロセス


### 🚫 話さないこと
- 自社サービス開発における事例
- AIエディタの機能・コスト比較
- 具体的なコーディング手法や実装例

---

![bg 90%](../../assets/images/2025/qiita-bash/organization.png)

<!-- _header: "" -->
<!-- _class: lead -->

<style scoped>
h3 {
  position: absolute;
  top: 65px;
  left: 0;
  right: 0;
  margin: auto;
  text-align: center;
  color: #0066cc;
  width: fit-content;
}
.black-text {
  color: black !important;
}
</style>

### [弊社サイト](https://jobs-3-shake.com/%e6%a0%aa%e5%bc%8f%e4%bc%9a%e7%a4%be%e3%82%b9%e3%83%aa%e3%83%bc%e3%82%b7%e3%82%a7%e3%82%a4%e3%82%af-%e6%8e%a1%e7%94%a8%e6%83%85%e5%a0%b1%e4%b8%ad%e9%80%94%e3%82%a8%e3%83%b3%e3%82%b8%e3%83%8b%e3%82%a2%e7%b3%bb%e8%81%b7%e7%a8%ae) <strong class="black-text">より</strong>

---

## 🖊️ [Cursor](https://www.cursor.com/ja)について

![bg right:20% 75%](../../assets/images/2025/qiita-bash/cursor.png)

- Visual Studio Codeをベースにした**AI統合型のコードエディタ**
- プロジェクト全体の**コードベースをインデックス化**し、</br>自然言語での検索やAIによるコーディングが可能
- Pro・Businessプランでは各種最新モデルを</br>月500まで**高速リクエスト**可能
- 以降はスローリクエストまたは従量課金
- 新しい[モデル](https://docs.cursor.com/models#models)が使える（最近もclaude-4-sonnetにすぐ対応）
- 無料で使えるモデルも多数  

---

![bg 80%](../../assets/images/2025/qiita-bash/cursor_plan.png)

---

## 👨‍💻 Cursorの導入

**導入に至った理由**
- Vibe codingの高まりを踏まえ、アプリケーションチームとしてAI活用推進したい
- 個人契約で使っているエンジニアも多く、導入してほしいという要望

**導入前の環境**
- 原則、各自が好みのエディタを使用（VS Code、Vim/Neovimなど）
- GitHub Copilot Business経由で各種最新モデルを利用可能
- 個人で任意のAIエディタ・エージェントを使用していたメンバーも多数

---

## 💼 懸念点：クライアントワーク

- **少人数単位での案件進行**
  - 案件あたり2-3名単位かつ、複数の業務が並走
- **案件ごとに異なる開発環境**
  - 言語、フレームワークなどが異なる
- **マネージドIDE環境制約**
  - Google Cloud Workstationなどの開発環境制限

---

## 🤖 懸念点：急速なAI環境の変化

![bg right:35% 70%](../../assets/images/2025/qiita-bash/overwhelmed.png)

<div class="small-text">

- **エンジニア個々の嗜好・習慣**
  - エディタ設定やプラグイン構成の個人最適化
  - [avante.nvim](https://github.com/yetone/avante.nvim)など**各コミュニティAIプラグイン**開発
- **AIコーディングツールの競争激化**
  - [Windsurf](https://windsurf.com/editor)（2024年 11月）
  - VS Code Agent Mode（2025 4月）
  - [Codex](https://openai.com/index/introducing-codex/)（2025年 5月）
  - [Claude Code](https://docs.anthropic.com/ja/docs/claude-code/overview)（2025年 5月）

</div>

---

## 🗓️ 1ヶ月後...どうなった？

メンバーにアンケートを依頼

---

## 👍 生産性の向上

- **実装スピード**が早くなった
  - コード補完（tab）
  - 自然言語によるコード生成・編集（Command K）
  - AIチャットによるコード相談・修正（Chatパネル）
- **コードベース全体を対象**とした質問により仕様理解が楽にあった
- **リファクタリングやテスト**の負担が減った
- コーディング以外にも**ドキュメンテーション作成**の補助になった

---

## 🌀 課題

- **機能認知の不足** </br>機能が多すぎて全てを把握しきれず、なんとなく使いこなせていない感覚に陥る
- **良すぎるUX** </br>基本機能が直感的で使いやすいため、詳細なドキュメンテーションを参照して</br>他の機能まで深く掘り下げる必要性を感じにくい
- **学習時間の確保困難** </br>ツールの具体的な使い方が個人の裁量に任されていたため、体系的な学習機会や</br>サポートが必要という声も

---

## ✅ 実際の浸透過程
![bg right:30% 90%](../../assets/images/2025/qiita-bash/notion.png)

<div class="small-text">

- 急激な変化ではなく、1ヶ月かけて**徐々に浸透**
- **社内Notionを活用した知見の蓄積**
  - Tips、案件事例、他社事例リンク、課題・要望
- **複数ツールの併用**
  - Vimと同じフォルダを開き、コードベース全体への</br>質問など特定の場面でCursorを活用
  - 特定の言語やプロジェクトでのみCursorを使用
    - PythonやTypeScriptはLLM自体の学習が進んでいる説
    - GoやPHPはあんまり？</br>（rulesをちゃんと書いた方がいいらしい）
    - [Awesome CursorRules](https://github.com/PatrickJS/awesome-cursorrules)
</div>

---

## 👀 VS Codeの動向とフォークエディタへの影響

- **VS Codeによる機能追従**
  - Cursor Composer（マルチファイル同時編集機能、2024年7月）</br>->GitHub Copilot Multi-file editing (2024年10月)
  - Cursor Agent Mode（2024年9月）</br>->VS Code Agent Mode（2025年4月）
- **基盤 VS Code バージョンの遅延**
  - Cursor は VS Code 1.96（2024 年11月）を基盤としており、</br>互換性問題も発生
- Microsoft製拡張機能の[**フォークIDE非対応化**](https://github.com/getcursor/cursor/issues/2976?ref=blog.lai.so)（2025年4月）
- VS Code [**GitHub Copilot Chat 拡張 OSS 化**](https://code.visualstudio.com/blogs/2025/05/19/openSourceAIEditor)（2025/5/19発表）

---

## 📝 まとめ

- **AI活用を促すきっかけ**としてのエディタのチーム導入は効果あり
- クライアントワークの特性や、エンジニアファーストの観点から単一AIエディタの</br>全面導入がマッチするとは限らない
  - 申請は**希望制**にしたり、**複数の選択肢**から選べるようにするのが理想
- 現状ベストは刻々と変わるので**AIツールをどう使い分けるかが重要**

---

## [Cursor Meetup Tokyo](https://aiau.connpass.com/event/353531/)

![bg right:40% 60%](../../assets/images/2025/qiita-bash/cursormeetup.png)

- 日本初のコミュニティイベント
- 参加者4000名オーバー！
- **日時**: 2025年6月6日（金）18:30〜21:30
- **場所**: 株式会社メルカリ+オンライン

---

<!-- 
_backgroundColor: #0a1929
_color: white
_class: title dark
-->

![bg](../../assets/images/3shake-background-full.png)

<!-- タイトルページ左上に大きなロゴを表示 -->
<div style="position: absolute !important; top: 5px !important; left: 5px !important; z-index: 9999 !important; margin: 0 !important; padding: 0 !important;">
  <img src="../../assets/images/3shake-logo.png" style="width: 240px !important; height: auto !important; display: block !important;">
</div>

<div style="text-align: center; margin-top: 200px;">

# ありがとう<span class="highlight-yellow">ございました</span>

### ご質問・ご相談はお気軽にお問い合わせください

@iorandd | https://3-shake.com
</div> 