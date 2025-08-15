私は独学でgitを扱っているため, 不足や誤りがあるかもしれない.
（指摘などはDMでお願いします. linkは一番下にあります）
tagやpull requestなどすべての機能を網羅していないことをご了承ください.

# メリット
- 無料で利用できる
- cloudでプログラムを管理できる
- バージョン管理ができる（編集履歴が残る）
- GitはCLIの入門になる
- 公開に向いている（プライベート設定もできる）

# 最初にやってほしいこと

まずアカウントを作りログインしてください.
ログインしてから読み進めることをお勧めします.

# 前提知識

Linkは以下のように表示されます.
[私のGitHub](https://github.com/Noot-cat)

表記が変化するものは下記のように表記します.
例:ユーザー名 `{{ユーザー名}}`

commentは基本プログラミング言語に従い, コメント記法が存在しない, もしくは私が知らない場合下記のように表記します.
例:コメント `#コメント`

GitHub単体だと効果は薄いので, Gitと組み合わせて使うとよい.
GitHubは大体「コードなどを見れる場所」で, Gitは大体「コマンド」という認識で大丈夫. (詳しくは他を参照)

## 用語
GItHubでは用語があり, 今回はすべてを網羅しているわけではないことに注意.

| 用語                     | 意味                                       |
| ------------------------ | ------------------------------------------ |
| `repository`(レポジトリ) | プロジェクトやファイルを管理する箱・土台   |
| `branch`(ブランチ)       | 作業内容ごとに分岐できる枝                 |
| `pull`(プル)             | GitHubから最新の変更を取得, ローカルに保存 |
| `push`(プッシュ)         | 変更内容をGitHubに送信                     |
| `commit`(コミット)       | 変更履歴を記録                             |
| `stage`(ステージ)        | 変更の記録対象として一時的に登録            |

## Git

### Gitのインストール

>[!warning] 注意
>ここで扱うのはWindowsのみである.

Gitはインストールしないと使えない.

1. Gitと検索して（多分）一番上の[Git/Downloads](https://git-scm.com/downloads)を開く. 
1. Latest source Releaseの[Download for Windows](https://git-scm.com/downloads/win)を押す.
1. インストーラー起動, 全部Nextでいい. (エラー吐くようだったら管理者権限で起動してみる)
1. インストールが完了したら, Git起動.

### Gitの設定

GitHubのログインを先にすること.

```cardlink
url: https://github.com/
title: "GitHub · Build and ship software on a single, collaborative platform"
description: "Join the world's most widely adopted, AI-powered developer platform where millions of developers, businesses, and the largest open source community build software that advances humanity."
host: github.com
favicon: https://github.githubassets.com/favicons/favicon.svg
image: https://images.ctfassets.net/8aevphvgewt8/4UxhHBs2XnuyZ4lYQ83juV/b61529b087aeb4a318bda311edf4c345/home24.jpg
```

ユーザー名とメールアドレスを設定する.
Git Bashを実行して、以下のコマンドを打ち込む.

ユーザー名の設定
```
git config --global user.name "{{ユーザー名}}"
```

メールアドレスの設定
```
git config --global user.email "{{メールアドレス}}"
```

SSHを作成.（公開鍵, 秘密鍵の作成）

```
ssh-keygen
```

SSHキーの保存先, パスワードを指定. デフォルトで問題ない場合は何も入力せずにEnterを押す.

表示内容
```
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/????/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

# GitHubの基本

## 最初

### レポジトリの作成

1. レポジトリ名を決める.（レポジトリ名は同じものを使えない）
1. （説明を入れる）
1. パブリックかプライベートかを選ぶ. （後で変えられるが, 今回は説明しない）
1. README.mdはパブリックならあるほうが優しい.（なくてもよい）

GitHub側は操作終わり

1. WindowsのPowerShell/Terminalを管理者権限で開く.
1. 管理したいフォルダに移動. （`cd {{フォルダのパス}}`）
1. (フォルダのパスは`ctrl+shift+c`でコピーできる.)
```
git init
git add README.md # 任意
git add * # 任意
# ただし, git add がないとコミットができないため, どちらかは実行すること.
git commit -m"first commit"
git branch -M main
git remote add origin {{URL}}.git # Quick setupのHTTPSをコピペのほうがミスがない
git push -u origin main
```

コメントなし
```
git init
git add README.md
git add *
git commit -m"first commit"
git branch -M main
git remote add origin 
git push -u origin main
```

### 解説

git init
- `.git`フォルダを作成
- これがないとGitHub/Gitが動かない

git add README.md
- README.mdを作成

git add *
- すべての変更をステージ
- \*は隠しファイル以外すべてという意味, これはパスでも可
- 隠しファイルもステージしたい場合, `git add .`で出来る

git commit -m "first commit"
- コミットをする.
- -m"{{comment}}"　ダブルクォーテーション内には好きにコメントを入れる. 入れないとエラーが起きる.

git branch -M main
- 今いるブランチを強制的にmainと名前を付ける. 昔はmasterが主流だった.
- -Mが強制的にあたる. 普段は-mを使うとよい.

git remote add origin 
- ローカルレポジトリ(PC側)とリモートレポジトリ(GitHub側)をつなぐ.

git push -u origin main
- mainをoriginにアップロードする.（GitHub側へ押す）
- -uは追跡関係（upstream）を設定する.

以降は `git push` や `git pull` だけでリモートリポジトリのmainブランチとやり取りできる. 毎回ブランチ名やリモート名を指定する必要がなくなる.

## 以降
```
git add *
git commit -m"{{メッセージ}}"
git push
git pull
```

基本的にこれしか使わない.
git pullはGitHub上の変更をローカルリポジトリに取得すること. 

GitHubから引く=pull
GitHubへ押す　=push　とイメージすればよいと思う.

# Gitの他のコマンド
```
git clone {{HTTPS}}
```

レポジトリを丸ごとcloneする. コミット履歴もcloneされる.

```
git checkout {{コミットID}}
```

コミット部分に行ける.（過去のコードに戻れる）

```
git fetch
```

GitHub側をローカルへ持ってくるが, ローカル側に反映されない.

### 複数人で開発する場合
```
git merge
```

マージ（ブランチの統合）をするときがある.
ブランチ同士の比較, 異なる部分を直す, mergeという流れ
異なる部分がある場合, 衝突（コンフリクト）が起こる.

コンフリクトマーカーが追加されるのでどちらかを残し, マーカーを消す.
```
<<<<<<< HEAD 

{mainブランチで変更した内容} 

=======

{otherブランチで変更した内容} 

>>>>>>> other
```

解消した後は
```
git add *
git commit -m"{{メッセージ}}"
(git push)
```
でコミットする.


# 最後に

Git/GitHubのすべてを網羅していないため進めていくうちにわからないことも出てくると思う. 
私は一人でgitを扱っているため, 複数人の場合について間違いがある可能性が大きい.

間違っている部分などは遠慮なく指摘してください.
もし複数人で使っている方がいるなら, 教えてくださるとありがたいです.

今後アウトプット用にこのようなものを書いていくと思います.
見てくださるとうれしいです

###### 作者
**Noot**

[Twitter](https://x.com/0001No2)
DMしても反応できないと思います.
[GitHub](https://github.com/Noot-cat)
[Discord](https://discord.gg/xXfqzvCYBS)
Discordは反応できます.
