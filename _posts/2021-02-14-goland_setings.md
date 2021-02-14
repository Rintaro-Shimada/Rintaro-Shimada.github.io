---
title:  Goland でgithubのプライベートリポジトリをgo mod 使う時の設定 
tags:
- Goland
- golang
- 開発
---
## Goland で go mod を使うときの注意
最近 golang で開発を始めたのですが、github のプライベートリポジトリで管理されているパッケージをgo mod とセットで使おうとしたところ
エラーが出てしましました。

{% highlight log %}
--------github のURL------- 410 Gone
{% endhighlight %}
みたいな感じで 410 というエラーが出ました。  
まず確認したのは、 Go env の設定です。

{% highlight log %}
GO111MODULE="on"
GOPROXY="direct"
GOSUMDB="off"
{% endhighlight %}

この三つののパラメーを確認したのですが、もちろん上記のようになっていて問題はなし、なので原因を探していたら
意図していない動作があるのがわかりました。package のインポートする際のダウンロード元にアクセスできない、プロキシの設定が無効になっているようでした。
けど、設定はしているのにおかしいと思っていたら、 GoLand は自陣のプロジェクトごとに環境設定を持っていて、その設定を読み込んでいたのです。

<div class="card mb-3">
    <img class="card-img-top" src="/upload_files/images/goland_env_seting.png"/>
    <div class="card-body bg-light">
        <div class="card-text">
            このようにに設定すると使えるかと思います。
        </div>
    </div>
</div>

てっきり私はシステムの方の設定を使っているのかと思っていました。
これを見つけたとき悔しかったです。
