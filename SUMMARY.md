# マイツール置き場(mytools) 進捗メモ 2026-07-11

> このファイルは元 `~/.claude/SUMMARY-mytools.md`(設定リポジトリ)に置かれていたものを、
> 本来の置き場所である mytools リポジトリへ移設(2026-07-13)。以後 mytools の作業サマリはここに書く。

## 何を作ったか
X で見た「MATO's Tools」を参考に、**自作ツールを1画面に集約する個人ハブ**を単一の自己完結HTMLで作成。サイドバー目次＋カード＋カードを押すと中でツールが開く構成。

- 公開URL: **https://fukushimak1207.github.io/mytools/**
- リポジトリ: **`fukushimak1207/mytools`(新規 public)** — GitHub Pages で公開済み
- ローカル: `~/projects/mytools/`(index.html / README.md / .gitignore)

## 内蔵ツール(すべて動作・localStorage 保存)
- 🧠 **マインドマップ** — ツリー整列・子/兄弟追加(Tab/Enter)・編集・削除・Markdown/JSON 書き出し
- ✅ **チェックリスト** — 進捗バー・**全部リセットで再利用**・複数リスト管理(見本「連休前チェック」)
- 📝 **メモ帳** — 自動保存・複数メモ・コピー
- 🔍 **用語・略語メモ** — 検索絞り込み・自分で追加(見本 CoNS/QC/TAT。要出典の判定値は意図的に未収録)
- カード: ねだん帳(実リンク) / 家計簿・検査当番表(プレースホルダ)

## 重要: 修正したバグと教訓
- **症状**: デスクトップでサイドバーが全幅表示、ハブのカードが見えず「押しても無反応」(ねだん帳リンクのみ動く)
- **原因**: `.scrim`(モバイル用の暗幕)が `.app` グリッドの最初の子なのに、desktop で `display:none` が未指定。グリッド1列目(248px)を空の暗幕が占領し、サイドバーが2列目=全幅へ、メインが暗黙の2行目(画面外)へ押し出されていた
- **修正**: CSS 基本ルールに `.scrim { display: none; }` を1行追加(`~/projects/mytools/index.html`)。実寸1280pxで sidebar=248px / main=1032px の2カラムを実測検証済み・push 済み
- **教訓**: 検証を狭い幅(モバイル)だけで済ませない。**必ず desktop 幅でも目視/実測する**

## Git 状態
- `~/projects/mytools`: commit 4本 push 済み・working tree clean。**サブPCには未 clone**
- Artifact でも公開(claude.ai、URL は会話内)

## サブPCで再開するとき
1. リポジトリを clone:
   ```
   cd "$env:USERPROFILE\projects"
   git clone git@github.com:fukushimak1207/mytools.git
   ```
2. 公開ページはそのまま使える: https://fukushimak1207.github.io/mytools/
3. 編集したら `index.html` を push → 1〜2分で公開反映

## 次にやりたいこと(候補)
- 家計簿カードに実 URL を差し込む(デプロイ先確認)
- 検査当番表ツールが完成したらリンク化
- マインドマップを自由配置ドラッグ/ズームに拡張、メモ帳の Markdown 表示
- チェックリストのテンプレ追加(機器立ち上げ・精度管理 など)

## 注意
- データは各ブラウザの localStorage 保存 → **PC間・Artifactと公開ページ間では同期されない**。大事な中身は各ツールのコピー/書き出しで持ち出す
- 公開ページに氏名「福島さん」が出る(ユーザーが「このまま公開」を選択)。消したくなったら index.html の挨拶とロゴを差し替え
