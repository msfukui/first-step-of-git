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

2020/07/28 @msfukui

---
class: center, middle

# 導入の目的

# ＝

# どんな課題を解消できる?

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

* バイナリファイルの管理 (Word, Excel, pdf, jpeg, png..)

    特に Word や Excel の変更は、それぞれのアプリケーション内の機能で管理した方がよさそう

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

## ソフトウェア開発プロセス全体への広がり

  * Pull Request (Merge Request) によるレビュー

  * コードの変更を契機としたビルド、テスト、リリース（デプロイ）の自動化 (CI/CDパイプライン)

      ピタゴラ装置っぽいの

      <img src="slides/cicd_pipeline.png" alt="Git" width="75%">

---

## 学ぶ価値のある人

<img src="slides/computer_programming_woman.png" alt="Git" width="15%">
<img src="slides/computer_programming_man.png" alt="Git" width="15%">

* ソフトウェア、アプリケーションのソースコードに何らか関わる人

    作る人だけでなく、テストする人、レビューする人、ドキュメントを書く人、承認する人..

* ITシステムのインフラを構築、保守運用する人にも

    ITインフラの構成をコードで表現する (Infrastructure as Code)

    ソフトウェア開発の手法をITインフラの構築・保守運用にも適用 (GitOps)

---

## 試してみる

### Gitlab

* ログイン

* プロファイルの編集

* Personal Access Token の払い出し

* 他のリポジトリを見てみる

  例: pester-example

* パスの形式（個人名・グループ名/リポジトリ名）

* README.md, Commit, Compare, Merge Request

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

    `git init` で、指定したディレクトリの配下全てが git の管理下になります。

    ```
    $ mkdir example
    $ cd example
    $ git init .
    Initialized empty Git repository in /.../example/.git/
    ```

    一番上のディレクトリには `.git` という管理用のディレクトリが作られます。

    ```
    $ ls -a
    .  ..  .git
    $
    ```

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

    \# 以下の `https://example.com/msfukui/example.git` は一例です。  
    \# 実際には、作成したリモートリポジトリの URL を指定してください。

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

    `-u` は現在のローカルリポジトリをリモートリポジトリに紐づけるためのオプションです。

    最初のリモートリポジトリへの反映の際にのみ指定します。

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

<p><small>※引用元: 【Git入門】git status の使い方（ファイルの状態を確認する） <a href="https://26gram.com/git-status">https://26gram.com/git-status</a></small></p>

---

### リモートリポジトリとローカルリポジトリ

<img src="slides/local_and_remote_repository.jpg" alt="local and remote repogitory" width="52%">

個々のPCには、ローカルリポジトリの他に、リモートリポジトリのコピーも保存されている

<p><small>※引用元: Gitが、おもしろいほどわかる基本の使い方33_Chapter1-02 <a href="https://www.mdn.co.jp/di/contents/3421/41576/">https://www.mdn.co.jp/di/contents/3421/41576/</a></small>

---

### コミットとコミットハッシュ

  ```
  $ git log
  commit 421ac8214a877dfdfb6eee1973b054b4d9d2b410 (HEAD -> master, origin/master)
  Author: msfukui <msfukui@gmail.com>
  Date:   Sun Jun 28 18:53:42 2020 +0900

      First commit
  ```

コミット単位で SHA-1 による一意キー（コミットハッシュ）が生成される

* ログにある `421ac...` の部分がコミットハッシュ

* 先頭4〜7文字だけでも有効 (short hash)

* Git は、コミット単位で変更を管理する

<p>
<small>※より詳しい仕組みを知りたい人は..<br />
Gitのコミットハッシュ値は何を元にどうやって生成されているのか | Mercari Engineering Blog<br />
<a href="https://tech.mercari.com/entry/2016/02/08/173000">https://tech.mercari.com/entry/2016/02/08/173000</a></small>
</p>

---

## Git の操作 (続き) (1/4)

* **取り消し**

    * ひとつ前をやり直す (commit --amend)

    * 取り消す (reset, revert)

* **ブランチとマージ**

    * ブランチの作成 (branch)

    * ブランチの移動 (checkout)

    * ブランチのマージ (merge)

---

## Git の操作概要 (続き) (2/4)

* **リモートリポジトリの操作**

    * リモートリポジトリから変更を取得する (pull)

    * リモートリポジトリに変更を反映する (push)

    * Merge Request の発行とマージ

---

## Git の操作概要 (続き) (3/4)

* コミットの整理

    * 複数のコミットを整理する (rebase)

    * 複数のコミットを一つにまとめる (squash)

* 歴史の改竄

    * リモートリポジトリを強制的に上書きする (push -f)

* 調べる

    * プロジェクト内のコードをまとめて grep する (grep)

* コミットに名前をつける (tag)

---

## Git の操作概要 (続き) (4/4)

* その他覚えておくと便利なもの

    * 編集中の内容を一時退避する (stash)

    * 特定のコミットの変更内容を抜き出して適用する (cherrypick)

* コマンド以外で理解しておきたいこと

    * first-forward (ff) と non-fast-forward (no-ff) の違い

    * リポジトリ管理の対象外のファイルリスト (.gitignore)

    * コミットの頻度

    * コミットログの書き方

    * コマンドエイリアス

---

## Git の操作 (取り消し)

### コミットをやり直す (commit --amend)

`README.md` に文章を追加して..

```
$ echo "" >> README.md
$ echo "## Hello, world" >> README.md
$ cat README.md
# Example

## Hello, world
```

---

変更したファイルをインデックス(ステージ)に上げて..

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
  modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
$ git add .
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
  modified:   README.md
```

\# `git add .` とすると、<br />
\# `.` (今のディレクトリ)の配下全部のファイルを、まとめてインデックスに上げることができます。

---

コミットしたが..

```
$ git commit -m "Add Hello, wrold"
[master a167513] Add Hello, wrold
 1 file changed, 2 insertions(+)
```

うっわ、コミットメッセージのスペル間違えた..🙍<br />
恥ずかしい..😓 どないしよ..

```
$ git log
commit a167513c86329587fa25184e0eb3be37524b723b (HEAD -> master)
Author: msfukui <msfukui@gmail.com>
Date:   Sat Jul 11 20:00:39 2020 +0900

    Add Hello, wrold

commit 6c14441ef60f2c0ba2a15464cae91dcb1e876bd4
Author: msfukui <msfukui@gmail.com>
Date:   Sat Jul 11 19:59:34 2020 +0900

    First commit
```

---

`git commit` のオプションの `--amend` を使うと、直前のコミットを取り消して、<br />
現在の状態で再度コミットをやり直すことができます。

```
$ git commit --amend -m "Add Hello, world"
[master a717807] Add Hello, world
 Date: Sat Jul 11 20:00:39 2020 +0900
 1 file changed, 2 insertions(+)
$ git log
commit a71780770b122aa800ef2d8f0a7793de4e168cdf (HEAD -> master)
Author: msfukui <msfukui@gmail.com>
Date:   Sat Jul 11 20:00:39 2020 +0900

    Add Hello, world

commit 6c14441ef60f2c0ba2a15464cae91dcb1e876bd4
Author: msfukui <msfukui@gmail.com>
Date:   Sat Jul 11 19:59:34 2020 +0900

    First commit
```

今の状態から追加で変更して、前のコミットと合わせてコミットを一つにする場合にも使えます。

---

### 変更をなかったことにする (reset)

`reset` は、現在の最新のコミットを、指定したある時点のコミットに変更するコマンドです。

指定方法によっては、これまでの変更内容が一部失われてしまう可能性があります。

特に、リモートリポジトリに `push` した後の `reset` は、他の人にも影響が及びます。<br />
他の人には影響がないと確信できる場合を除き、原則はできないと思った方がよいです。

使用上の注意をよく読み、用法・用量を守って正しくお使いください。🏥💊

<p>
<small>※とても説明がわかりやすいので、実行する前には一度読んでおくことをお勧めします。<br />
c.f. [git reset (--hard/--soft)]ワーキングツリー、インデックス、HEADを使いこなす方法 - Qiita<br />
<a href="https://qiita.com/shuntaro_tamura/items/db1aef9cf9d78db50ffe">https://qiita.com/shuntaro_tamura/items/db1aef9cf9d78db50ffe</a></small>
</p>

---

`reset` は以下の様に指定します。

```
$ git reset [(1)ワークツリー、インデックスをどうしたいか?] [(2)最新のコミットをどこにしたいか?]
```

(1) は以下のオプションから設定します。

* `--soft` は、インデックス(ステージ)まで戻します。

* `--mixed` (デフォルト) は、ワークツリーまで戻します。

* `--hard` は、ワークツリー、インデックスともなかった状態に戻します。

    \# 変更が全て吹っ飛ぶので危険! 指定は慎重に!

(2) はどこまで戻すかを、コミットハッシュまたはコミットを示す別名(エイリアス)で指定します。

* `HEAD` は、最新のコミットを指し示す別名(エイリアス)です。

* `HEAD^` は、ひとつ前のコミットを指し示す別名(エイリアス)です。

* `HEAD^^^` (三つ前)なども指定できます。

---

#### `reset` よく使う例

* コミット状態をひとつ前のコミットに戻して、そこからの変更はインデックスに上がった状態にする

    ```
    $ git reset --soft HEAD^
    ```

    追加で変更してコミットし直すだけなら `commit --amend` を使う方が楽かもしれないです。

* コミット状態をひとつ前のコミットに戻して、そこからの変更はワークツリーに戻す

    ```
    $ git reset HEAD^
    ```

* コミット状態をひとつ前のコミットにして、そこからの変更は全部消す

    \# 危険! 実行時は注意!

    ```
    $ git reset --hard HEAD^
    ```

---

* 現在インデックス(ステージ)に上がっている状態を全てワークツリーに戻す

    ```
    $ git reset HEAD
    ```

* 最新のコミット状態に戻して、そこからの変更点は全てなかったことにする

    \# 危険! 実行時は注意!

    最後のコミットからのワークツリー、インデックス(ステージ)の内容を消し飛ばします。

    ```
    $ git reset --hard HEAD
    ```

* **[重要]** 直前の `git reset` を取り消す (取り消しの取り消し)

    ```
    $ git reset --hard ORIG_HEAD
    ```

    `ORIG_HEAD` は前回 `reset` した際の `HEAD` を指しています。

    \# これで戻せなかったら詳しい人を呼んで一緒に泣きましょう..。

---

### 変更を明示的に打ち消す (revert)

`revert` は特定のコミット、マージを明示的に打ち消すためのコミットを新しく生成します。

`reset` は編集内容がコミットログには一切残りませんが、 `revert` はこれまでのコミットログは残したまま、コミットを新しく生成する（積み上げる）ところが異なります。

```
$ git revert a167513
[master 6cfab82] Revert "Add Hello, world"
 1 file changed, 2 deletions(-)
$ git log
commit 6cfab82b59e89d6407b9935d930f5e89b027c96c (HEAD -> master)
Author: msfukui <msfukui@gmail.com>
Date:   Mon Jul 27 20:13:35 2020 +0900

    Revert "Add Hello, world"

    This reverts commit a71780770b122aa800ef2d8f0a7793de4e168cdf.
...
```

（わかりにくいですが） `hello.rb` の追加が、打ち消されてコミット前の状態に戻っています。

---

## ブランチとマージ

### ブランチ = **「枝」**

変更前のコミットに影響を与えずに、複数の人が並行して編集できる様にするための仕組み。

実態は「任意のコミットに対して付けられる名前」（ポインタ）

<img src="slides/branch_image.png" alt="branch" width="75%">

<p><small>※引用元: git ブランチを合流するマージ: プログラマの歩き方 <a href="http://zorinos.seesaa.net/article/451407561.html">http://zorinos.seesaa.net/article/451407561.html</a></small></p>

---

```
$ git branch testing
```

<img src="slides/head-to-master.png" alt="branch" width="75%">

<p><small>※引用元: Git - ブランチとは<br /><a href="https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E6%A9%9F%E8%83%BD-%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E3%81%A8%E3%81%AF">https://git-scm.com/book/ja/v2/Git-のブランチ機能-ブランチとは</a></small></p>

---

```
$ git checkout testing
```

`git checkout -b testing` で branch と checkout をまとめて一つのコマンドで実行することもできます。

<img src="slides/head-to-testing.png" alt="branch" width="75%">

---

```
$ vim test.rb
...
$ git add test.rb
$ git commit -m 'made other changes'
```

ひとつコミットすると、testing ブランチと現在の最新のコミット (HEAD) がひとつ先に進みます。

<img src="slides/advance-testing.png" alt="branch" width="75%">

---

```
$ git checkout master
```

HEAD が指すコミットを master に移動します。

履歴が一旦巻き戻った様に見えます。

<img src="slides/checkout-master.png" alt="branch" width="75%">

---

```
$ vim test.rb
...
$ git add test.rb
$ git commit -m 'made another changes'
```

さらに別の内容をひとつコミットして master を進めると、変更の履歴が二つに分岐します。

<img src="slides/advance-master.png" alt="branch" width="75%">

---

### マージ

マージは、複数のブランチをまとめて一つにします。

```
$ git merge [マージしたいブランチ名]
```

#### オートマージに成功した場合

```
$ git merge testing
Merge made by the 'recursive' strategy.
hello.rb |    1 +
1 file changed, 1 insertion(+)
```

<p>
<small>※Git のマージ戦略の詳細を知りたい方は..<br />
アルゴリズム - Git の 3-way merge とは具体的にどのようなアルゴリズムですか？ - スタック・オーバーフロー<br />
<a href="https://ja.stackoverflow.com/questions/52019/git-%E3%81%AE-3-way-merge-%E3%81%A8%E3%81%AF%E5%85%B7%E4%BD%93%E7%9A%84%E3%81%AB%E3%81%A9%E3%81%AE%E3%82%88%E3%81%86%E3%81%AA%E3%82%A2%E3%83%AB%E3%82%B4%E3%83%AA%E3%82%BA%E3%83%A0%E3%81%A7%E3%81%99%E3%81%8B">https://ja.stackoverflow.com/questions/52019/git-の-3-way-merge-とは具体的にどのようなアルゴリズムですか</a></small>
</p>

---

#### コンフリクトした場合

```
$ git merge testing
Auto-merging hello.rb
CONFLICT (content): Merge conflict in hello.rb
Automatic merge failed; fix conflicts and then commit the result.
$ cat hello.rb
puts 'Hello, world'
<<<<<<< HEAD
puts 'See you tomorrow!'
=======
puts 'Good by'
>>>>>>> testing
```

* どこがコンフリクトしているかは示してくれる

    * 上記の `<<<<<<<` から `>>>>>>>` で区切られた行

    * 複数の行の塊がコンフリクトすることもあり得る

* コンフリクトの解消には、手で直して add して commit しないといけない

    有効なのは HEAD? testing? 両方とも有効? 両方ともだめ? 一部だけ?

---

## リモートリポジトリの操作

(再掲)

<img src="slides/local_and_remote_repository.jpg" alt="local and remote repogitory" width="52%">

---

### リモートリポジトリから変更を取得する (pull)

```
$ git pull origin master
```

リモートの `origin` リポジトリの `master` ブランチの内容を取得して、<br />
ローカルリポジトリの `master` ブランチにマージする。

### リモートリポジトリに変更を反映する (push)

```
$ git push origin master
```

ローカルリポジトリの `master` ブランチの内容を、<br />
リモートの `origin` リポジトリの `master` ブランチにマージする。

---

### Merge Request の発行とマージ

Gitlab の画面から、リモートリポジトリのブランチをマージするリクエストを発行することができます。

<img src="slides/gitlab_merge_request.png" alt="gitlab merge request" width="80%">

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

無料で読める Git のマニュアルには以下があります。

* 「Git - Book」

    https://git-scm.com/book/ja/v2

Progate の Git のコースはとてもよい評価をお聞きしました。(n = 2)

* Git ソースコードのバージョン管理や共同開発を可能にするツール

    https://prog-8.com/languages/git

* ドットインストール https://dotinstall.com/lessons/basic_git もいいかもです。

GitHub を使った共同開発については、以下の書籍が参考になります。(お貸しできます！）

* 「GitHub 実践入門」

    https://gihyo.jp/book/2014/978-4-7741-6366-6
