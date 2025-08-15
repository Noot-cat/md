私は独学でgitを扱っているため、不足や誤りがあるかもしれない。指摘などはDMでお願いしたい（リンクは一番下に記載）。tagやpull requestなどすべての機能を網羅していないことを了承されたい。

# メリット

- 無料で利用できる
- cloudでプログラムを管理できる
- バージョン管理ができる（編集履歴が残る）
- GitはCLIの入門となる
- 公開に適している（プライベート設定も可能）

# 最初にやってほしいこと

最初にアカウントを作成し、ログインしておくことを推奨する。ログイン後に読み進めることが望ましい。

# 前提知識

Linkは以下のように表示される。
[私のGitHub](https://github.com/Noot-cat)

表記が変化するものは下記のように記述する。
例:ユーザー名 `{{ユーザー名}}`

コメント記法は基本プログラミング言語に従い、コメント記法が存在しない、もしくは私が知らない場合、下記のように記述する。
例:コメント `#コメント`

GitHub単体だと効果は薄いため、Gitと組み合わせて使うのが望ましい。
GitHubは「コードなどを見れる場所」、 Gitは「コマンドによる操作」という認識で問題ない。(詳細は他資料も参照)

## 用語
GitHubには様々な用語が存在する。ここではすべてを網羅していない点に留意すること。

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
>ここで扱うのはWindowsのみを対象とする.

Gitはインストールしないと利用できない。

1. Gitと調べ、[Git/Downloads](https://git-scm.com/downloads)を開く。
1. [Download for Windows](https://git-scm.com/downloads/win)をクリックする。
1. インストーラを起動し、「Next」を連打で基本的に問題ない。（エラーが生じた場合、管理者権限で再実行すること）
1. インストール完了後、Git Bashを起動する。

もしここでエラーが継続して発生する場合は、自身で対処を試みるだけでなく、私に連絡するか、AIにエラー内容を送信し対応すること

### Gitの設定

必ずGitHubへのログインを先に済ませておくこと。

```cardlink
url: https://github.com/
title: "GitHub · Build and ship software on a single, collaborative platform"
description: "Join the world's most widely adopted, AI-powered developer platform where millions of developers, businesses, and the largest open source community build software that advances humanity."
host: github.com
favicon: https://github.githubassets.com/favicons/favicon.svg
image: https://images.ctfassets.net/8aevphvgewt8/4UxhHBs2XnuyZ4lYQ83juV/b61529b087aeb4a318bda311edf4c345/home24.jpg
```

Git Bashを実行して、以下のコマンドを打ち込む。

ユーザー名の設定
```
git config --global user.name "{{ユーザー名}}"
```

メールアドレスの設定
```
git config --global user.email "{{メールアドレス}}"
```

SSHキーを作成（公開鍵と秘密鍵の作成）

```
ssh-keygen
```

SSHキーの保存先、パスワードを指定する。 デフォルトで問題ない場合は何も入力せずにEnterを押す。

表示内容
```
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/????/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

作成後、生成された公開鍵（例：`id_rsa.pub`）の中身をコピーし、 GitHubの"Settings"→"SSH and GPG keys"で新しいSSHキーとして登録すること。
これにより、今後はパスワード無しで安全にリモート操作を行うことができる。

# GitHubの基本

## 最初

### レポジトリの作成

1. レポジトリ名を決める。（重複は不可、mainも避けるとよい）
1. 必要に応じて説明文を設定する。
1. パブリックかプライベートかを選択する。 （後から変更可能であるが、今回は割愛）
1. README.mdはパブリックリポジトリの場合、作成しておくとよい。（省略も可）

>[!tips] README.mdの意義
>README.mdがあると、リポジトリの意図が他者に伝わりやすくなる。自身が意図を忘れた際の備忘録にもなるため、極力記載することを推奨する。

ここまでがGitHub上での操作である。

1. PowerShell/Terminalを管理者権限で起動する。
1. 管理対象のフォルダに移動する。（`cd {{フォルダのパス}}`。パスは`ctrl+shift+c`でコピー可能）

```
git init
git add README.md # 任意
git add * # 任意
# いずれかのgit addを実行しないとコミットは不可。
git commit -m "first commit"
git branch -M main
git remote add origin {{URL}}.git  # Quick setupのHTTPSをコピーして貼り付けるとよい。
git push -u origin main
```

### 解説

git init
- `.git`フォルダを作成し、以降Gitで履歴管理が可能となる。

git add README.md
- README.mdのみをステージする

git add *
- 隠しファイル以外のファイルをすべてステージ対象とする。`*`はシェルが自動的に展開し、「.」で始まるファイル（隠しファイル）は含まれない。
- すべてを確実に加えたければ、`git add .` または `git add -A` を推奨する。

git commit -m "first commit"
- 作業履歴を「first commit」のコメントとともに記録する。コメントが未設定の場合、エラーとなる。
- このコメントは任意の内容に自由に変更可能である。日本語も対応している。


git branch -M main
- 現在のブランチ名をmainに強制変更する（従来はmasterが主流）。`-M`で強制適用、通常は`-m`でよい。

git remote add origin 
- ローカルリポジトリとリモートレポジトリ（GitHub）を紐付ける。

git push -u origin main
- mainブランチをGitHub上のoriginへ初回アップロードし、追跡関係も設定する（以後は`git push`のみでよい）。

以降は`git push`や`git pull`のみでmainブランチとのやりとりが可能となる。以後、リモート名やブランチ名を省略できる。

## 以降の基本コマンド
```
git add *
git commit -m"{{メッセージ}}"
git push
git pull
```

主に上記以外は使わない。

- `git pull`はGitHub側の変更をローカルリポジトリに取得する。

- GitHubから取得（pull）、GitHubに送信（push）というイメージを持つとよい。

# Gitの他のコマンド
```
git clone {{HTTPS}}
```

リモートリポジトリをコミット履歴ごとクローンする。

```
git checkout {{コミットID}}
```

過去の特定のコミット内容に切り替える。

```
git fetch
```

リモートの状態をローカルに取得するが、作業ディレクトリには反映されない。

### 複数人で開発する場合
```
git merge
```

複数のブランチを統合する際に使用する。差分でコンフリクト（衝突）が起こる場合は、手動で解消する必要がある。

コンフリクトを起こすとマーカーが追加される
```
<<<<<<< HEAD 

{mainブランチの内容} 

=======

{otherブランチの内容} 

>>>>>>> other
```

上記マーカー内を修正し、マーカー自体を削除後、以下を実行して反映する。
```
git add *
git commit -m"{{メッセージ}}"
(git push)
```

で変更を反映する。

# 最後に

本資料ではすべての機能や運用方法を網羅していない。進めながら疑問や不明点が発生した場合は、適宜調査・質問してほしい。  
誤りや改善点についてはご指摘を歓迎する。複数人で使用されている方は、共有いただけるとありがたい。

今後もアウトプットを目的としてこの種の資料を作成する予定である。読んでいただけると幸いである。

###### 作者
**Noot**

[gmail](Noot.cat.contact@gmail.com)
[Twitter](https://x.com/0001No2)
[GitHub](https://github.com/Noot-cat)
[Discord](https://discord.gg/xXfqzvCYBS)

連絡はgmailまたはDiscordでお願いしたい。
