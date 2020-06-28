class: center, middle

<style>
.two-column-left{
  float: left;
  width: 40%;
  text-align: left;
}
.two-column-right{
  float: right;
  width: 55%;
  text-align: left;
}
</style>

<style>
.column-left{
  float: left;
  width: 50%;
  text-align: left;
}
.column-right{
  float: right;
  width: 50%;
  text-align: left;
}
</style>

<img src="slides/git.svg" alt="Git" width="20%">

# Git

## 最初の一歩

2020/07/02 @msfukui

---
class: center, middle

## 導入の目的

## ＝

## どんな課題を解消できる?

---

## どこかでみたことある

<img src="slides/filename_version_control.png" alt="ファイル名でバージョン管理" width="100%">

---

## よりスマートに

* 複数のファイルの変更をまとめて管理

* 任意のある時点に戻す／取り消す／戻すのを取り消す

* 複数の人が同時に編集してもいい感じにする

  * 複数の人が同時に行った変更の衝突（コンフリクト）を検出したり

  * できるだけ頑張って自動で解消したり（オートマージ）

### 背景

* プロダクトの変更のサイクルはどんどん上がっている

  もっと素早く、でも安全に変更したい

---

## 歴史

* Linux のソースコード管理のために実装されたのが始まり

  それまで使われていた別の構成管理ツールの代替として OSS で開発されている

* 現在ではソースコード管理のデファクト・スタンダードとなっている

---

## 比較

### 得意なこと

* テキストファイルの管理

  差分での比較が簡単にできる (diff)

### 苦手なこと

* バイナリファイルの管理

  Word, Excel, pdf, jpeg, png, ..

  特に Word や Excel の変更は、それぞれのアプリケーション内の機能で管理した方がよさそう

---

## Git と GitHub, Gitlab

* <img src="slides/git.svg" alt="Git" width="5%"> Git https://git-scm.com

  Git の実装。ツール本体。Git の利用に必須。

* <img src="slides/github.svg" alt="GitHub" width="5%"> GitHub https://github.com

  Github, inc. が提供している Git のホスティングサービス。開発に便利な付加機能が多く提供されている。

  オンプレミスにインストール可能なソフトウェア (Github Enterprize(GHE)) も提供されている。

* <img src="slides/gitlab.svg" alt="Gitlab" width="5%"> Gitlab https://about.gitlab.com

  OSS で開発されている GitHub に似たソフトウェアの一つ。貧者の GHE と揶揄されることも。

  オンプレミスにインストールできる他、Gitlab, inc. が提供しているホスティングサービスもある。

---

## 用語

* コミット

  ある時点の中身をまとめて保存すること

* ブランチ

  任意のコミットに対して付けられる名前

* マージ

  複数のコミットを一つにまとめること

* コンフリクト

  マージの際に同じファイルの編集が重なって変更内容が衝突すること

* タグ

  ブランチとは別に任意のコミットに対して付けられる別名

---

## 試してみる

### Gitlab

* ログイン

* プロファイルの編集

* Personal Access Token の払い出し

* 他のリポジトリを見てみる

  例: pester-example

* パスの形式（個人名・グループ名/リポジトリ名）

* README.md, Compare, Issue, Merge Request

---

### Git for Windows

* インストール

* 設定

  * `git config` の設定

  * `.netrc` の設定

* Gitlab からのリポジトリの clone

  例: pester-example

* github.com からのリポジトリの clone

  例: https://github.com/tokyo-metropolitan-gov/covid19

---

### Git の操作

* ディレクトリ作成と初期化 (init)

* README.md の編集

* 状態を確認 (status)

* インデックスに追加 (add)

* 確定 (commit)

* ログを見る (log)

* Gitlab にリポジトリを作る & リモートリポジトリを登録 (remote add origin)

* リモートリポジトリに反映 (push)

* Gitlab で確認する

---

## Git の仕組み

### ワークツリーとインデックスとリポジトリ

<img src="slides/worktree_index_repository.png" alt="How Git works" width="70%">

---

### ローカルリポジトリとリモートリポジトリ

<img src="slides/local_and_remote_repository.jpg" alt="local and remote repogitory" width="65%">

---

### コミットハッシュ

  ```
  $ git log
  commit 421ac8214a877dfdfb6eee1973b054b4d9d2b410 (HEAD -> master, origin/master)
  Author: msfukui <msfukui@gmail.com>
  Date:   Sun Jun 28 18:53:42 2020 +0900

      First commit
  ```

---

## Git の操作 (続き)

### 戻す

* 変更をなかったことにする (reset)

* 変更を明示的に取り消す (revert)

---

### ブランチとマージ

* ブランチの作成 (branch)

* ブランチの移動 (checkout)

* 編集, status, add, commit, log

* リモートリポジトリから変更を取得する (pull)

* リモートリポジトリに変更を反映する (push)

* Merge Request の発行 → merge

---

### もっと使ってみる

* 歴史を変える

  複数のコミットを整理する (rebase)

  複数のコミットを一つにまとめる (squash)

  リモートリポジトリを強制的に上書きする (push -f)

* 調べる

  プロジェクト内のコードをまとめて grep する (grep)

* その他

  tag, stash, cherrypick

---
class: center, middle

# Enjoy, DevOps!

---

# 参考

以下から画像を借用させていただきました。

* 【Git入門】git status の使い方（ファイルの状態を確認する）

  https://26gram.com/git-status

* Gitが、おもしろいほどわかる基本の使い方33_Chapter1-02

  https://www.mdn.co.jp/di/contents/3421/41576/

無料で読める Git のマニュアルには以下があります。

* 「Git - Book」 https://git-scm.com/book/ja/v2

GitHub のエコシステムを使った開発は以下の書籍が参考になります。

* 「GitHub 実践入門」 https://gihyo.jp/book/2014/978-4-7741-6366-6
