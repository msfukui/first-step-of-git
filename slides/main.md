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

* 複数のファイルの変更をまとめて履歴管理

* 任意のある時点に戻す／戻すのを取り消す

* 複数の人が同時に編集してもいい感じにする

  * 複数の人が同時に行った変更の衝突（コンフリクト）を検出したり

  * できるだけ頑張って自動でいい感じに解消したり

### 背景

* ソフトウェア = ソースコードの変更のサイクルはどんどん上がっている

  もっと素早く、でもできるだけ安全に変更したい

---

## 歴史

<img src="slides/linux_tux.svg" alt="Linux Tux" width="15%">

* Linux のソースコード管理のために実装されたのが始まり

  過去使われていた別の構成管理ツールの代替として OSS で開発されている

* 現在ではソースコードを管理するツールのデファクト・スタンダード

* ソースコード以外のファイル構成管理にも利用が広がっている

  テキスト・ドキュメント、アセット（画像、スタイルシートなど）

---

## 得意なことと苦手なこと

### 得意なこと

* テキストファイルの管理

  差分での比較が簡単にできる (diff)

  複数の変更の衝突を自動で解消したり(auto merge)

### 苦手なこと

* バイナリファイルの管理

  Word, Excel, pdf, jpeg, png, ..

  特に Word や Excel の変更は、それぞれのアプリケーション内の機能で管理した方がよさそう

---

## 学ぶ価値のある人

* ソフトウェア、アプリケーションのソースコードに何らか関わる人

  作る人だけでなく、テストする人、レビューする人、リリースを承認する人も

  ITシステムを構築、保守運用する人も

### なぜ?

* ソースコードの変更管理だけではない広がり

  * Pull Request (Merge Request) によるレビュー

  * 変更を契機としたビルド、テスト、リリース（デプロイ）の自動化 (CI/CDパイプライン)

  * ITインフラの構成をコードで表現する (Infrastructure as Code)

---

## Git と GitHub, Gitlab

<img src="slides/git.svg" alt="Git" width="5%"> Git https://git-scm.com

  Git の実装。ツール本体。Git の利用に必須。

<img src="slides/github.svg" alt="GitHub" width="5%"> GitHub https://github.com

  Github, inc. が提供している Git のホスティングサービス。開発に便利な付加機能が多く提供されている。

  オンプレミスにインストール可能なソフトウェア (Github Enterprize(GHE)) も提供されている。

<img src="slides/gitlab.svg" alt="Gitlab" width="5%"> Gitlab https://about.gitlab.com

  OSS で開発されている GitHub に似たソフトウェアの一つ。# 貧者の GHE と揶揄されることも。

  オンプレミスにインストールできる他、Gitlab, inc. が提供しているホスティングサービスもある。

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

* インストール https://gitforwindows.org/

* Git Bash の起動

    ```
    $ git --version
    git version 2.27.0.windows.1
    ```

Git の本体は git というコマンドライン・ツールです。

git コマンドにサブコマンドを指定して操作します。

```
$ git help
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
          [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
          [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
          [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
          <command> [<args>]
...
```

---

### 初期設定と動作確認

* 初期設定

  * `git config` の設定

  * `.netrc` の設定

  * mitty の設定

* 動作確認: リモートからコードを取ってきてみる (clone)

  * Gitlab から

      例: pester-example

  * github.com から

      ```
      $ git clone https://github.com/tokyo-metropolitan-gov/covid19.git
      ```

---

### Git の操作 (1/7)

README.md というファイルを一つ持つプロジェクトを新規に作成して、git で管理してみます。

* ディレクトリ作成と初期化 (init)

    ```
    $ mkdir example
    $ cd example
    $ git init .
    Initialized empty Git repository in /.../example/.git/
    ```

作成したディレクトリの配下全てが git の管理下になります。

---

### Git の操作 (2/7)

* README.md の作成

    ```
    $ echo "# Example" > README.md
    $ ls
    README.md
    $ ls
    $ cat README.md
    # Example
    ```

`.md` は Markdown というテキストファイル形式の拡張子です。

簡易の文書作成のためのフォーマットとして広く使われています。

c.f. https://commonmark.org

---

### Git の操作 (3/7)

* 状態を確認 (status)

    ```
    $ git status
    On branch master

    No commits yet

    Untracked files:
      (use "git add <file>..." to include in what will be committed)
      README.md

    nothing added to commit but untracked files present (use "git add" to track)
    ```

---

### Git の操作 (4/7)

* インデックス（ステージ）に追加 (add)

    ```
    $ git add README.md
    $ git status
    On branch master

    No commits yet

    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)
      new file:   README.md
    ```

---

### Git の操作 (5/7)

* 確定 (commit)

    ```
    $ git commit -m "First commit"
    [master (root-commit) f38a5e9] First commit
    1 file changed, 1 insertion(+)
    create mode 100644 README.md
    ```

`-m` は一行コメントのためのオプションです。コメントは、変更内容や理由を記述するために使われます。

* コミットログを見る (log)

    ```
    $ git log
    commit f38a5e96fba32bdfbcba6fa1027082b8b1354cc2 (HEAD -> master)
    Author: msfukui <msfukui@gmail.com>
    Date:   Tue Jun 30 20:24:44 2020 +0900

        First commit
    ```

コミットログの表示は、複数あると、最新のものから表示されます。

---

### Git の操作 (6/7)

* Gitlab にリポジトリを作る & リモートリポジトリを登録 (remote add origin)

    先に Gitlab のトップ画面から New Project でリモートリポジトリを新規に作成します。

    ```
    $ git remote add origin https://example.com/msfukui/example.git
    $ git remote show origin
    * remote origin
      Fetch URL: https://example.com/msfukui/example.git
      Push  URL: https://example.com/msfukui/example.git
      HEAD branch: (unknown)
    ```

---

### Git の操作 (7/7)

* リモートリポジトリに反映 (push)

    ```
    $ git push -u origin master
    Enumerating objects: 3, done.
    Counting objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 216 bytes | 216.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To https://example.com/msfukui/example.git
    * [new branch]      master -> master
    Branch 'master' set up to track remote branch 'master' from 'origin'.
    ```

    `-u` は現在のローカルリポジトリをリモートリポジトリに紐づけるための設定です。

    最初のリモートリポジトリへの反映にのみ指定します。

Gitlab の画面から変更内容が反映されていることを確認できれば完了です。

お疲れ様でした！🙌

---

## 用語説明

* リポジトリ (Repository)

  Git の管理対象となる複数のファイルのかたまり

* コミット (commit)

  ある時点の中身をまとめて保存すること

* マージ (merge)

  複数のコミットを一つにまとめること

* コンフリクト (conflict)

  マージの際に同じファイルの編集が重なって変更内容が衝突すること

* ブランチ (branch)

  任意のコミットに対して付けられる名前

---

## Git の仕組み

### ワークツリーとインデックス(ステージ)とリポジトリ

<img src="slides/worktree_index_repository.png" alt="How Git works" width="70%">

---

### ローカルリポジトリとリモートリポジトリ

<img src="slides/local_and_remote_repository.jpg" alt="local and remote repogitory" width="52%">

個々のPCには、ローカルリポジトリの他に、リモートリポジトリのコピーも保存されている

---

### コミットハッシュ

  ```
  $ git log
  commit 421ac8214a877dfdfb6eee1973b054b4d9d2b410 (HEAD -> master, origin/master)
  Author: msfukui <msfukui@gmail.com>
  Date:   Sun Jun 28 18:53:42 2020 +0900

      First commit
  ```

* コミット単位で SHA-1 による一意キー（コミットハッシュ）が生成される

    ログにある `421ac...` の部分

    先頭4〜7文字だけでも有効 (short hash)

* より詳しい仕組みを知りたい人は..

    Gitのコミットハッシュ値は何を元にどうやって生成されているのか | Mercari Engineering Blog

    https://tech.mercari.com/entry/2016/02/08/173000

---

## Git の操作 (続き)（※次回があれば..）

### 戻す

* 変更を明示的に取り消す (revert)

* 変更をなかったことにする (reset)

### やり直す

* 確定（コミット）をやり直す (commit --amend)

---

### ブランチとマージ

* ブランチの作成 (branch)

* ブランチの移動 (checkout)

* リモートリポジトリから変更を取得する (pull)

* リモートリポジトリに変更を反映する (push)

* ブランチのマージ (merge)

* Merge Request の発行 → merge

---

### コミットの整理

  複数のコミットを整理する (rebase)

  複数のコミットを一つにまとめる (squash)

### 歴史の改竄

  リモートリポジトリを強制的に上書きする (push -f)

---

### 調べる

  プロジェクト内のコードをまとめて grep する (grep)

### その他

  * tag, stash, cherrypick

  * first-forward (ff) と non-fast-forward (no-ff)

  * .gitignore

  * コミットログの書き方

---

## その他

### テキストエディタどうする?

最低限、文字コード UTF-8、改行コード &lt;LF&gt; が扱えるもの

* メモ帳: 🙅 最近強化されているみたいですが..

* Git Bash に添付のエディタ: Vim

* 他の選択肢: Windows だと..

    * サクラエディタ

    * 秀丸

    * Visual Studio Code

---

## 参考

以下から画像を借用させていただきました。

* 【Git入門】git status の使い方（ファイルの状態を確認する）

  https://26gram.com/git-status

* Gitが、おもしろいほどわかる基本の使い方33_Chapter1-02

  https://www.mdn.co.jp/di/contents/3421/41576/

無料で読める Git のマニュアルには以下があります。

* 「Git - Book」 https://git-scm.com/book/ja/v2

GitHub のエコシステムを使った開発は以下の書籍が参考になります。(お貸しできます！）

* 「GitHub 実践入門」 https://gihyo.jp/book/2014/978-4-7741-6366-6
