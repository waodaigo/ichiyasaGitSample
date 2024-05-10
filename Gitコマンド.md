# GitコマンドではないがGitBashで使うコマンド

## 特殊なディレクトリの記法

### カレントディレクトリ

- 「.」（ドット）

### ホームディレクトリ

- 「~」（チルダ）

### ルートディレクトリ

- 「/」（スラッシュ）

## ディレクトリを操作する基礎的なコマンド

### カレントディレクトリの絶対パスを表示（コマンドプロンプトでは使えない）

- $ pwd

### 新しいディレクトリを作成する

- $ mkdir ディレクトリパス

### ディレクトリ内容を確認する（コマンドプロンプトでは使えない）

- $ ls オプション ディレクトリパス

    - 例：$ ls  
    何もつけないとカレントディレクトリの中を表示

    - 例：$ ls -a  
    オプションがないと表示されなかったディレクトリやファイルが表示される

    - 例：$ ls Documents  
    ディレクトリパスをつけるとカレントディレクトリを移動せずにDocumentsの中身を表示。

### カレントディレクトリを移動する

- $ cd ディレクトリパス

    - $ cd ../  
    で一つ上の階層に移動


## エディタを起動してディレクトリを開く

### ディレクトリを指定する

- $ code /c/users/sanmple


### 現在のディレクトリを指定する

- $ code .




# GitHub周りのコマンド

## SSH Keyの生成

- $ ssh-keygen -t rsa -b 4096 -C "メールアドレス"

    - 例：$ ssh-keygen -t rsa -b 4096 -C "daigo@gmail.com"

## 公開鍵をクリップボードにコピー（Windows）

- $ clip < 鍵のパス

    - 例：$ clip < /c/Users/daigo/.ssh/id_rsa/id_rsa.pub  
    ただクリップボードにコピーするだけなのでファイルを直接開いてコピーしてもよい。

## 確認用コマンド

- $ ssh -T git@github.com

その後「yes」と入力し、設定したパスワードを打つ。  
Hi ユーザー名! You've successfully authenticated,  
と出たら成功

# Gitコマンド

## バージョン確認

**git --version**  
または  
**git --v**

## 設定の追加、変更、確認

### 設定の確認

**git config 設定項目名**  


#### 設定値の一覧を表示

- $ git config --list  


表示しきれないときは「:」が表示されるのでキーボードの上下でスクロールする。エンターキーでも進める。  
「Q」キーを押すとコマンドラインに戻る。

#### ユーザー名の確認

- $ git config user.name  

#### メールアドレスの確認

- $ git config user.email  

### 設定を追加や変更

**git config --global 設定項目名 設定値**  

--global オプションをつけないとローカルリポジトリ固有の設定を行う。  
ローカルリポジトリが優先される。

#### グローバルのユーザー名の設定

- $ git config --global user.name ユーザー名

    - 例：$ git config --global user.name Daigo

#### ローカルのユーザー名の設定

- $ git config user.name ユーザー名

    - 例：$ git config user.name Daigo

以後、--globalオプションは省略してローカルのみ説明する。  

#### メールアドレスの設定

- $ git config user.email メールアドレス

    - 例：$ git config user.email daigo@gmail.com

## ローカルリポジトリを作成

**git init**  

ローカルリポジトリを作成したいカレントディレクトリに移動してコマンドを実行する。  

## ローカルリポジトリの状態を確認

**git status**  

## ファイルをステージングエリアへ登録

**git add ファイルパス**  

### ファイルを登録

- $ git add ファイルパス

    - 例：$ git add Git_MEMO.md
        - これだとカレントディレクトリのGit_MEMO.mdのみ登録する。  
        この場合だと相対パスとなる。
    - 例：$ git add subDirectory/Git_MEMO2.md
        - これだとsubDirectory内のGit_MEMO2.mdのみ登録する。

### カレントディレクトリ配下のファイルをすべて登録

- $ git add .

### ディレクトリ配下のファイルをすべて登録

- $ git add ディレクトリパス

    - 例：$ git add subDirectory

### ファイルをまとめてステージングエリアへ登録

- $ git add -A

## ファイルの差分を確認

**git diff**  

### ワークツリーとステージングエリアの差分を表示

- $ git diff

### ステージングエリアとGitディレクトリの差分を表示

- $ git diff --cached

### 現在チェックアウトしているブランチと他のブランチとの差分を表示

- $ git diff 他のブランチ名

    - 例：$ git add master

## ファイルをコミット

**git commit**  

### オプションなしだとコミット時にエディタを開いてコメントを入力する

- $ git commit

### コミットメッセージを指定してコミット

- $ git commit -m "コミットメッセージ"  
  メッセージは" "で囲んで指定

    - 例：$ git commit -m ".gitignoreファイルを追加する"

### ステージングエリアへの登録とコミットを実行

- $ git commit -a

ステージングエリアへの登録とコミットを同時に実行する。

### ステージングエリアへの登録とコミットメッセージを指定してコミット

- $ git commit -am "コミットメッセージ"

    - 例：$ git commit -am ".gitignoreファイルを追加する"

### 直前のコミットを変更し新しいコミットへ置き換え

- $ git commit --amend

直前のコミットを変更して、新しいコミットに置き換える。コミットメッセージの変更や、コミットし忘れた変更を直前のコミットに加えることができる。  
原則としてプッシュすることができなくなる。

### 直前のコミットメッセージを変更

- $ git commit --amend -m "コミットメッセージ"

    - 例：$ git commit --amend -m "変更後のコミットメッセージ"

## 特定のバージョンをワークツリーへ反映

**git checkout**  

### ワークツリーの変更を取り消し

- $ git checkout -- ファイル / ディレクトリパス

    - 例：$ git checkout -- Git_MEMO.md

パラメーターにブランチ名ではなく -- を指定すると直前のコミットの状態に戻す。  
ステージ登録前に行う。  
ファイルの新規作成やファイル名変更は取り消せない。

### ブランチを切り替え

- $ git checkout ブランチ名

    - 例：$ git checkout update-venue

使用するブランチを、指定したブランチに切り替える。フェッチしたばかりでローカルリポジトリに存在しないブランチを指定した場合、ブランチの作成も行う。

### 名前を指定して新しいブランチを作成

- $ git checkout -b 新しいブランチ名

    - 例：$ git checkout -b speakers-info

指定した名前で新しいブランチを作成する。作成元のブランチは、現在使用中のブランチになる。

### 作成元のブランチを指定して新しいブランチを作成

- $ git checkout -b 新しいブランチ名 チェックアウト元のブランチ名

    - 例：$ git checkout -b speakers-info master

作成元のブランチを指定して、指定した名前で新しいブランチを作成する。現在使用中のブランチに関わらず、同じブランチが作成元となる。

## ローカルリポジトリの状態を戻す

**git reset**  

### ファイルをステージングエリアからワークツリーへ戻す

- $ git reset HEAD ファイルパス

    - 例：$ git reset HEAD Git_MEMO.md  
    $ git reset HEAD . もできた。

指定したファイルがステージングエリアからワークツリーへ戻る。HEADとは、最後にコミットした状態を指す。

### 指定したコミットまで取り消し

- $ git reset --soft コミット

    - 例：$ git reset --soft HEAD~

ワークツリーとステージングエリアは変更されない。コミットハッシュの変更をするので、すでにプッシュしたコミットには実行しないことが望ましい。たとえば、HEAD~（HEADの一つ前のコミット）を指定して実行すると、HEADを取り消してコミットをHEAD~まで戻す。直前のコミットでGit_MEMO.mdを変更していた場合、結果としてステージングエリアにGit_MEMO.mdの変更が登録されている状態になる。コミットの指定には、ハッシュ値を用いることも可能。

### 指定したコミットまで（ステージングエリアへの登録も）取り消し

- $ git reset --mixed コミット

    - 例：$ git reset --mixed HEAD~

### 指定したコミットまで（ワークツリー、ステージングエリアへの登録も）取り消し

- $ git reset --hard コミット

    - 例：$ git reset --hard HEAD~


## ファイルを削除

**git rm**  

### ワークツリーからファイルを削除（コミットはしない）

- $ git rm ファイルパス

    - 例：$ git rm remove_me.txt

ワークツリーからファイルを削除し、削除した状態をステージングエリアへ登録。

### ワークツリーからディレクトリを削除（コミットはしない）

- $ git rm -r ディレクトリパス

    - 例：$ git rm -r subDirectory

ワークツリーからディレクトリを削除し、削除した状態をステージングエリアへ登録。

### ファイルやディレクトリをGitの管理下から外す（削除はしない）

- $ git rm --cached ファイルパス

    - 例：$ git rm --cached remove_me.txt

- $ git rm --cached -r ディレクトリパス

    - 例：$ git rm --cached -r subDirectory

指定したファイルやディレクトリをGitの管理下から外し、その状態をステージングエリアへ登録。ワークツリーからは削除されないため、ファイル自体は残る。


## コミット履歴を表示

**git log**

### コミット履歴を新しい順に表示

- $ git log

### 差分とコミット履歴を新しい順に表示

- $ git log -p

表示しきれないときは「:」が表示されるのでキーボードの上下でスクロールする。エンターキーでも進める。  
「Q」キーを押すとコマンドラインに戻る。


## リモートリポジトリをコピー

**git clone**

### リモートリポジトリをコピー

- $ git clone リモートリポジトリのURL

    - 例（SSH）：$ git clone git@github.com:ichiyasa-g/ichiyasaGitSample.git
    - 例（HTTPS）：$ git clone https://github.com/ichiyasa-g/ichiyasaGitSample.git


### ディレクトリを作成してリモートリポジトリをコピー

- $ git clone リモートリポジトリのURL ディレクトリ名

    - 例（SSH）：$ git clone git@github.com:ichiyasa-g/ichiyasaGitSample.git sampleDirectory

## リモートリポジトリの設定を変更、確認

**git remote**

### リモートリポジトリの設定を確認

- $ git remote -v

### 指定したURLのリモートリポジトリを設定に追加

- $ git remote add リモートリポジトリ名 リモートリポジトリのURL

    - 例：$ git remote add shiga git@github.com:shiga-iyg/ichiyasaGitSample.git

### リモートリポジトリの設定を削除

- $ git remote remove リモートリポジトリ名

    - 例：$ git remote remove origin

指定した名前のリモートリポジトリの設定を削除する。リモートリポジトリとしての設定が削除されるのみで、そのリモートリポジトリ自体が削除されるわけではない。

### リモートリポジトリの名前を変更

- $ git remote rename 変更前のリモートリポジトリ名 変更後のリモートリポジトリ名

    - 例：$ git remote rename shiga origin


## ブランチの作成、変更、削除、確認

**git branch**

### ブランチを作成

- $ git branch 新しいブランチ名

    - 例：$ git branch update-venue

### ブランチを一覧表示

- $ git branch

### マージ済みのブランチを削除（どちらでもいい）

- $ git branch --delete ブランチ名

    - 例：$ git branch --delete update-venue

- $ git branch -d ブランチ名

    - 例：$ git branch -d update-venue

指定したマージ済みのブランチを削除する。マージ済みではない場合、警告が表示され削除に失敗する。なお、現在使用中のブランチを削除したい場合は、実行前に1 度別のブランチをチェックアウトする必要がある。使用中のブランチは削除することができない。

### マージ状況にかかわらずブランチを削除

- $ git branch -D ブランチ名

    - 例：$ git branch -D update-venue

指定したブランチを削除する。ブランチがマージ済みかどうかにかかわらず、必ず削除に成功する。なお、現在使用中のブランチは削除することができない。使用中のブランチを削除したい場合は、実行前に1度別のブランチをチェックアウトする必要がある。

### ブランチの名前を変更

- $ git branch -m 変更前のブランチ名 変更後のブランチ名

    - 例：$ git branch -m update-venue update-event-venue

