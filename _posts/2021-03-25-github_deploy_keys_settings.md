---
title:  Git hub で デプロイキーを複数セットする時のサーバー側の設定  
tags:
- Git hub
- 開発
- デプロイ
---
# 複数デプロイキーが必要になる環境  
今までは、サーバーにつき一つのリポジトリしかなくバッティングしませんでした。ですが、同じ pub key を登録しようとすると  
`その鍵は使われている`という警告が出て登録できません。
解決方法は簡単で必要のリポジトリ分の鍵を生成してそれを使うのですが、普通にやっても使えませんでした。

1. .ssh/ 内でキーを生成 秘密鍵の名前を config ファイルに記述します。
```bash
Host {秘密鍵の名前}
  HostName github.com
  IdentityFile ~/.ssh/{秘密鍵の名前}
  User git
  TCPKeepAlive yes
  IdentitiesOnly yes
```

2. 公開鍵を Git hub の設定ページでデプロイキーをセット

3. サーバー側でコマンドを実行  
git clone
```bash
git clone git@{秘密鍵の名前}:{User_name}/{リポジトリー名}.git
```
git pull
```bash
git pull git@{秘密鍵の名前}:{User_name}/{リポジトリー名}.git
```

おそらくこれでできるかと思います。  
自分は管理が面倒くさかったので、リポジトリ名で鍵を作成しそれを記述しています、