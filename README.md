# ニュースダッシュボード

毎朝10時に自動更新される、スピントロニクス・IOWN／日本経済／B型支援準備の3カテゴリーをまとめたダッシュボードです。

## 公開URL

- GitHub Pages: https://chairo-chairo.github.io/news-dashboard/
- GitHubリポジトリ: https://github.com/chairo-chairo/news-dashboard

## ファイル構成

- `index.html` … ダッシュボード本体（Tailwind CSSを使った単一HTMLファイル）
- このフォルダ（`study/news`）にある `index.html` が「正本（マスター）」です。毎朝の自動更新もこのファイルを書き換えたあと、GitHubへpushしています。

## カテゴリー構成

1. **スピントロニクス・IOWN** … 本日・前日の2日分を切り替え表示。MRAM・光電融合関連ニュースと、関連銘柄（東京エレクトロン、キヤノン、アドバンテスト、ルネサス、TDK、信越化学、NTT、ニッチ銘柄、ETF）の株価を掲載。
2. **日本経済ニュース（週間まとめ）** … 直近1週間の為替・金利・株式市場の注目ニュースと、売買代金上位20銘柄（スピントロニクス・IOWNで注目している銘柄は⭐でハイライト）。
3. **B型支援 立ち上げ準備** … 就労継続支援B型の開設準備向けに、制度改正・特性のある子どものニュース・放課後等デイ関連ニュース・福祉現場のAI活用事例をまとめたもの。常に最新の内容に総入れ替え。

各カテゴリーに、それぞれ専用の「おすすめリンク集」があります。

## データの仕組み

ダッシュボードのニュース・株価データは、`index.html` 内の以下の部分にJSON形式で埋め込まれています。

```html
<script id="dashboard-data" type="application/json"> ... </script>
```

このJSONを書き換えることで、表示内容を更新できます（HTMLの見た目やJavaScriptのロジックは変更不要）。

## 自動更新の仕組み

- 毎朝10時に、Cowork（Claude）のスケジュールタスク「spintronics-iown-daily-briefing」が自動実行されます。
- タスクの内容: ①3カテゴリーのニュースをウェブ検索 → ②`index.html` 内のJSONを更新 → ③GitHubへpush → ④チャットで内容を報告。
- pushすると、GitHub Pagesが自動的にサイトへ反映します（反映まで数十秒〜数分）。

## GitHub連携について

- リポジトリへの書き込みには、GitHubのfine-grained personal access token（`news-dashboard` リポジトリに対する Contents: Read and write 権限）を使用しています。
- トークンはスケジュールタスクの設定ファイル内に保存されています。セキュリティの観点から、定期的な見直しや、不要になったタイミングでの失効（revoke）をおすすめします。
- トークンを再発行した場合は、スケジュールタスクの設定を更新する必要があります。

## 手動で更新したいとき

Claudeに「ダッシュボードを更新して」「GitHub Pagesにも反映して」と伝えれば、上記と同じ手順（JSON更新→push）を手動でも実行できます。
