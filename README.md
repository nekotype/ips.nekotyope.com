# 猫型iPS細胞研究所

note と X への案内を目的とした、ビルド不要の静的サイトです。HTML / CSS / SVG を基本とし、アクセス解析用のGoogleタグ（gtag.js）のみJavaScriptを使用しています。GTM・外部フォント・ビルドツールは使用していません。

## ローカルで見る

`index.html` をブラウザーで開いてください。インストールやビルドは不要です。
必要なら、このフォルダーで `python -m http.server 8080` を実行し、http://localhost:8080/ を開けます。

## ファイル

- `index.html`：本文、外部リンク、SEO・OGP設定、装飾アイコン、GA4のGoogleタグ
- `privacy.html`：Google Analyticsの利用と情報の取り扱いについて
- `css/style.css`：レスポンシブレイアウト、カードのホバー・キーボードフォーカス、動きを減らす設定への対応
- `assets/cat-face.svg`：タイトルとファビコンに使う猫の顔
- `assets/bichon.svg` / `cat-walking.svg` / `crow-flying.svg`：独立した動物シルエット
- `assets/ogp.png`：SNS共有用の画像（1200 × 630）
- `CNAME`：独自ドメイン `ips.nekotype.com`
- `.nojekyll`：GitHub PagesでJekyll処理を行わず静的ファイルを配信

動物はCSSの `.crow` / `.walking-cat` / `.bichon` で位置・サイズを変更できます。
表示文字はHTMLのテキストです。装飾のカテゴリ・動物・アイコンは読み上げ対象から外し、リンクはキーボード操作できます。外部リンクは同じタブで開きます。

## GitHub Pagesへの公開

1. GitHubにリポジトリを作成し、このフォルダーのファイル一式をルートにアップロードします。GitHub Freeの場合は公開リポジトリを使用します。
2. リポジトリの **Settings → Pages → Build and deployment** で、Sourceを **Deploy from a branch** にします。
3. Branchをアップロード先（例：`main`）、フォルダーを **/ (root)** に指定し、Saveを押します。
4. **Custom domain** に `ips.nekotype.com` を設定して保存します。リポジトリの `CNAME` も同じ内容で維持してください。
5. 下記のDNS設定を行い、PagesのDNSチェックとHTTPS証明書の発行が完了したら **Enforce HTTPS** を有効にします。反映には時間がかかることがあります。
6. https://ips.nekotype.com/ でPC・スマートフォン表示、note・Xへのリンク、共有画像を確認します。

公開先リポジトリ：https://github.com/nekotype/ips.nekotyope.com 。サイトのファイルはアップロード済みです。Pagesの有効化と独自ドメイン・HTTPSの設定は完了しています。リポジトリ名と独自ドメイン名は異なりますが、独自ドメインは `ips.nekotype.com` を使用します。

## 独自ドメインのDNS設定

GitHub側でCustom domainを設定した後、`nekotype.com` を管理するDNSサービスで以下を設定します。

| 項目 | 設定値 |
| --- | --- |
| レコード種別 | CNAME |
| 名前 / ホスト | `ips`（サービスによっては `ips.nekotype.com`） |
| 値 / 宛先 | `nekotype.github.io` |
| TTL | DNSサービスの既定値 |

公開先アカウントは `nekotype` です。DNSの宛先に `https://` やリポジトリ名、パスは含めません。

旧WordPress向けの `ips` のA / AAAA / CNAMEレコードがある場合は、その内容を控え、切り替え時に置き換えます。同じホスト名にCNAMEとA / AAAAを併存させないでください。ルートの `nekotype.com` やメールのMXレコードを変更する必要はありません。

PowerShellで確認する例：

```powershell
Resolve-DnsName ips.nekotype.com -Type CNAME
```

カスタムドメインの所有権確認も推奨します。GitHubアカウントの **Settings → Pages → Add a domain** で `nekotype.com` を追加し、案内されたTXTレコード名・値をDNSへ設定してVerifyします。確認用TXTは維持してください。GitHubが表示する値をそのまま使用します。

## 編集と更新

本文やリンクは `index.html`、デザインは `css/style.css` を編集します。更新したファイルを公開ブランチへ反映するとPagesが再公開します。独自ドメインを変更する場合は `CNAME` とcanonical・OGPのURLも合わせて変更してください。SNS共有画像を変更する場合は `assets/ogp.png` を差し替えます。

旧記事のURLは今回の1ページ構成に含みません。必要な旧記事は切り替え前にWordPressからバックアップしてください。

## 公式資料

2026年10月25日にGitHub公式資料を確認しました。

- [公開元ブランチを設定する](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [カスタムドメインを設定する](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
- [ドメインの所有権を確認する](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)

## Google Analytics 4

- 測定ID：`G-LGYK0YFJ6L`
- `index.html` の `<head>` に非同期のGoogleタグ（gtag.js）を直接設置しています。GTMは使用していません。`googletagmanager.com/gtag/js` はGoogleタグの正規の配信URLです。
- `gtag('config', 'G-LGYK0YFJ6L')` によって、トップページ読み込み時の `page_view` を自動送信します。二重送信を避けるため、手動の `page_view` や独自のクリックイベントは追加していません。
- note・Xは通常の外部リンクとして維持しています。GA4の拡張計測が有効なら、クリックを `click` イベントとして自動計測し、`link_url`、`link_domain`、`outbound` などで判別できます。
- 管理画面で **管理 → データストリーム → 対象のウェブストリーム → 拡張計測機能 → 歯車 → 離脱クリック** がオンになっていることを確認してください。管理画面の項目名は表示言語により「外部リンクのクリック」等の場合があります。この設定はHTMLから有効化できません。
- `note.com`・`x.com` をクロスドメイン測定の対象に追加しないでください。対象にすると離脱クリックの計測対象外になります。
- 設定後はリアルタイムレポートで `page_view` と `click` を確認できます。広告ブロックやブラウザーの追跡防止機能により計測されない場合があります。
- フッターからプライバシーポリシーへ移動できます。プライバシーポリシーページにも同じ測定IDのタグを1つ設置し、ページビューを計測します。

公式資料：[Googleタグの設置](https://developers.google.com/tag-platform/gtagjs)、[ページビュー計測](https://developers.google.com/analytics/devguides/collection/ga4/views)、[離脱クリックの計測](https://support.google.com/analytics/answer/13566436?hl=ja)。


導入時の検証（2026年10月29日）：ブラウザー上でGoogleタグを読み込み、`page_view` とnote・Xそれぞれの `click`（`outbound=true`）が生成されることを確認しました。検証イベントは送信直前に捕捉し、GA4には送っていません。GA4管理画面のレポート受信状況は未確認です。


## 旧WordPress URLの案内と計測

公開ルートの `404.html` をGitHub Pagesが存在しないURLに対して返します。HTTPステータスは404のままで、サーバー側の301リダイレクトは使いません。旧記事かどうかを判別する一覧はないため、旧記事以外の存在しないURLも同じ対象です。

1. `window.location.pathname` を取得し、GA4の `legacy_url_visit` イベントの `legacy_path` に送信します。パスはブラウザーの値をそのまま使い、日本語などはパーセントエンコードされた形式になる場合があります。
2. Googleタグを読み込む前にアドレスからクエリ・フラグメントを除外し、GA4の `page_location` もクエリのないURLに明示設定します。`page_referrer` は空にし、404ページのReferrer-Policyも `no-referrer` にしています。元のクエリをトップページの参照元として送らないための対策です。
3. 404ページでもGoogleタグによる `page_view` が発生します。旧パス別の集計には専用の `legacy_url_visit` イベントを使用します。転送後のトップページは既存のGoogleタグで通常どおり計測し、トップページ側のコードは変更しません。
4. イベントの処理コールバック後に100ms待って `location.replace('/')` で移動します。タグが読み込めない場合も約1.5秒で移動する独立したタイマーを設けています。送信・GA4側の受信は保証されません。バックグラウンドタブ等ではブラウザーのタイマー制限により長くなる場合があります。
5. JavaScript無効時は自動転送・計測を行わず、常時表示しているトップページへのリンクを使えます。
6. `noindex, nofollow` を設定しています。深い階層でも画像・リンクが壊れないよう、404ページではルートからの絶対パスを使います。

### 公開後のテスト

1. 実際に利用していた旧記事のURL（例：`https://ips.nekotype.com/2020/01/old-article/`）へアクセスします。存在しないテスト用パス `/__legacy-test__/sample-article/` でも確認できます。
2. 約1.5秒以内を目安に `https://ips.nekotype.com/` へ移動することを確認します。ブラウザーの開発者ツールのNetworkで **Preserve log（ログを保持）** を有効にすると、元のリクエストが404、移動先が200であることを確認できます。
3. GA4のリアルタイムレポートで `legacy_url_visit` を確認します。必要ならTag Assistantを使ってDebugViewでも確認できます。
4. Networkで `collect` を検索し、`en=legacy_url_visit`、`tid=G-LGYK0YFJ6L`、`ep.legacy_path=/2020/01/old-article/` を確認します。パラメータはURLデコード後の値で読みます。
5. クエリ除外の確認には `https://ips.nekotype.com/__legacy-test__/sample-article/?email=privacy-test%40example.invalid#test-fragment` のような **架空の値** を使用してください。イベントの `legacy_path` が `/__legacy-test__/sample-article/` のみであり、GA4への通信の `dl`（ページURL）、`dr`（参照元）や転送先にも、元のクエリ・フラグメントが含まれないことを確認します。実際の個人情報をテストに使わないでください。
6. Googleタグのリクエストを開発者ツールでブロックしてもトップへ移動すること、JavaScriptを無効にすると404ページに留まって手動リンクで移動できることを確認します。
7. 既存のトップページの `page_view` とnote・Xの `click` は従来どおりです。トップページや実在する `privacy.html` へのアクセスで `legacy_url_visit` が発生しないことも確認します。

ローカルで `404.html` を直接開くと、元の旧記事パスでの検証にはなりません。`python -m http.server` も既定ではカスタム404を返さないため、任意パスからの転送は公開サイトまたは404フォールバック対応のテストサーバーで確認してください。

`/?p=123` のように記事IDがクエリ文字列だけに含まれる旧URLは、トップページが存在するため404にならず、この仕組みの対象外です。クエリからの記事ID収集も行いません。トップページ側の既存GA4設定は変更していません。

### GA4で旧記事パス別に集計する設定

イベントの送信だけでは、`legacy_path` を通常のレポート・探索で使うためのカスタム定義は作成されません。GA4管理画面で次を一度登録します（編集者以上の権限が必要です）。

1. **管理 → データの表示 → カスタム定義 → カスタムディメンションを作成** を開きます。
2. ディメンション名：**旧記事パス**、範囲：**イベント**、イベントパラメータ：**`legacy_path`** で保存します。
3. **探索 → 自由形式** で行に「旧記事パス」、値に「イベント数」を置き、イベント名が `legacy_url_visit` と完全一致する条件で絞り込みます。

登録・データ収集後、レポートで利用できるまで24〜48時間かかる場合があります。管理画面にはこの作業環境からアクセスできないため、カスタムディメンションの登録は別途行ってください。

公式資料：[GitHub Pagesのカスタム404](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-custom-404-page-for-your-github-pages-site)、[Googleタグのイベントコールバック](https://developers.google.com/tag-platform/gtagjs/reference/parameters)、[イベント単位のカスタムディメンション](https://support.google.com/analytics/answer/14239696?hl=ja)。



### 全ページのページビュー計測（2026年10月30日）

`index.html`・`privacy.html`・`404.html` は同じ測定ID `G-LGYK0YFJ6L` で計測します。各HTMLのタグは1つで、`config` による自動 `page_view` を使い、手動 `page_view` は追加していません。SPAではなくページごとの通常のブラウザー遷移なので、履歴の監視や独自の画面遷移イベントも追加していません。404からトップへの転送では別々のページとしてそれぞれ1回計測し、既存の `legacy_url_visit` とクエリ除外処理は維持します。

公開後はGA4のリアルタイムレポート、または開発者ツールのNetwork（ログ保持）で `/`・`/index.html`・`/privacy.html` を開き、`collect` 通信の `en=page_view`、`tid=G-LGYK0YFJ6L`、`dl` のページURLを確認してください。1回のページ読み込みにつき `page_view` が1件であることを確認します。広告ブロックやブラウザーの追跡防止機能によって計測されない場合があります。
