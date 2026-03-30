# strataix-checkers デプロイ手順

作業時間の目安: 約15分（DNS反映は別途1〜24時間）

---

## 📁 フォルダ構成（現在）

```
strataix-checkers/
├── index.html          ← チェッカーシリーズ TOP LP
├── CNAME               ← checker.strataix.net（変更不要）
├── DEPLOY.md           ← このファイル
├── ai-work/
│   └── index.html      ← AIワーク相性チェッカー
├── moterudo/
│   └── index.html      ← 好かれ度チェッカー
└── shokuba/
    └── index.html      ← 職場適性チェッカー
```

**公開後のURL:**
- TOP: `checker.strataix.net/`
- AIワーク: `checker.strataix.net/ai-work/`
- 好かれ度: `checker.strataix.net/moterudo/`
- 職場適性: `checker.strataix.net/shokuba/`

---

## STEP 1 — ファイルをGitHubにプッシュ（GitHub Desktop）

> ⚠️ `.gitattributes` しか上がっていない場合はここから

1. GitHub Desktop を開く
2. 左上のリポジトリが `strataix-checkers` になっていることを確認
3. 左側の「**Changes**」タブに `index.html` や `ai-work/` などが表示されているはず
4. 「**Select All**」またはすべてにチェックを入れる
5. 下部の Summary に `add: チェッカーシリーズ 3本` と入力
6. 「**Commit to main**」をクリック
7. 右上の「**Push origin**」をクリック

GitHubの `strataix-checkers` リポジトリを開いて `index.html` が表示されていれば成功。

---

## STEP 2 — GitHub Pages 有効化

1. GitHub の `strataix-checkers` リポジトリを開く
2. **Settings → Pages**（左サイドバー）
3. Source: **Deploy from a branch**
4. Branch: **main** / **/ (root)** → **Save**
5. 数分待つと以下でアクセスできる（カスタムドメイン設定前）:
   - `https://[GitHubユーザー名].github.io/strataix-checkers/`

---

## STEP 3 — Firebase DNS に CNAME レコードを追加

`strataix.net` は Firebase（Google Domains）で管理されているため、DNS設定はここで行う。

### Firebase Console での手順

1. [Firebase Console](https://console.firebase.google.com) を開く
2. `strataix.net` のプロジェクトを選択
3. 左メニュー → **Hosting** → **Add custom domain**（または既存ドメインの DNS 管理へ）

### Google Domains（Squarespace）での手順

Firebase 経由で取得したドメインは **Google Domains → Squarespace Domains** に移管されている場合あり。

1. [domains.squarespace.com](https://domains.squarespace.com) を開く
   （または Google アカウントで Google Domains にログイン）
2. `strataix.net` を選択
3. **DNS → カスタムレコード（Custom records）**
4. 以下を追加:

| タイプ | ホスト名 | 値（Value） | TTL |
|--------|---------|------------|-----|
| CNAME | `checker` | `strataix.github.io` | 3600 |

5. 保存

> ⏱ 反映に最大24時間かかることがある（通常30分〜2時間）

---

## STEP 4 — GitHub Pages にカスタムドメインを設定

1. GitHub の `strataix-checkers` → Settings → Pages に戻る
2. **Custom domain**: `checker.strataix.net` を入力 → **Save**
3. DNS チェックが通ると「✅ DNS check successful」と表示される
4. **Enforce HTTPS** にチェックが入っていることを確認

> ⚠️ CNAMEファイルはすでにリポジトリに含まれているので手動作成は不要

---

## STEP 5 — 動作確認

- [ ] `https://checker.strataix.net/` → TOP LP が表示される
- [ ] `https://checker.strataix.net/ai-work/` → AIワーク相性チェッカーが表示される
- [ ] `https://checker.strataix.net/moterudo/` → 好かれ度チェッカーが表示される
- [ ] `https://checker.strataix.net/shokuba/` → 職場適性チェッカーが表示される
- [ ] HTTPS（鍵マーク）が表示される

---

## 新しいチェッカーを追加するとき

1. `strataix-checkers/[新フォルダ名]/index.html` を作成
2. `strataix-checkers/index.html`（TOP LP）のカードに追記
3. StratAIX LP（`strataix-website/`）のWebツール行にカード追加
4. GitHub Desktop でコミット＆プッシュ → Pages に自動反映（1〜2分）

---

## 完了後

- [ ] tasks.md のチェッカーシリーズタスクを ✅ に更新
- [ ] X / note でリリース告知
- [ ] Google Search Console に `checker.strataix.net` を追加登録（任意）
