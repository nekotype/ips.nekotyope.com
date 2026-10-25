# 猫型iPS細胞研究所

note と X への案内を目的とした、ビルド不要の静的サイトです。HTML / CSS / SVG のみで動作し、JavaScript・外部フォント・外部ライブラリは使用していません。

## ローカルで見る

`index.html` をブラウザーで開いてください。インストールやビルドは不要です。
必要なら、このフォルダーで `python -m http.server 8080` を実行し、http://localhost:8080/ を開けます。

## ファイル

- `index.html`：本文、外部リンク、SEO・OGP設定、装飾アイコン
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

この作業ではGitHubへのアップロード、Pagesの有効化、DNSの変更は行っていません。

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
