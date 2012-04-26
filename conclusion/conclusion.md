!SLIDE bullet small
## 以上が、Git を構成する要素の(ほぼ)全てです
* リポジトリ
* オブジェクトデータベース
* インデックス
* リファレンス

!SLIDE bullet incremental smaller
## ここまでの低レベルな観点だけで、<br/>下記の高レベルな視点に<br/>自分なりの回答ができるはずです
* いくら分散しても矛盾が発生しない理由
* ブランチの切り替えが高速な理由
* reflog で過去のどの時点にも戻れる理由
* 差分はどこから取り出しいつ計算するか推測
* SHA-1 ハッシュ値が衝突時に Git はどう振る舞うか推測

!SLIDE smaller
# おまけ
## SHA-1 ハッシュ値の衝突について小噺
<blockquote>
SHA-1 の衝突を見るにはどうしたらいいのか、ひとつの例をごらんに入れましょう。<br/>
地球上の人類 65 億人が全員プログラムを書いていたとします。そしてその全員が、Linux カーネルのこれまでの開発履歴 (100 万の Git オブジェクト) と同等のコードを一秒で書き上げ、馬鹿でかい単一の Git リポジトリにプッシュしていくとします。これを五年間続けたとして、SHA-1 オブジェクトの衝突がひとつでも発生する可能性がやっと 50% になります。<br/>
それよりも「あなたの所属する開発チームの全メンバーが、同じ夜にそれぞれまったく無関係の事件で全員オオカミに殺されてしまう」可能性のほうがよっぽど高いことでしょう。
</blockquote>
[ProGit 6.1 リビジョンの選択](http://progit.org/book/ja/ch6-1.html) より

!SLIDE 
# まとめ
* git のデータ構造はとてもシンプル
* 低レベルな視点を持つと高レベルな機能・問題は自然とわかるようになる

!SLIDE bullet smaller
# 参考資料(掘り下げたい人向け)
* [Git をボトムアップから理解する](http://keijinsonyaban.blogspot.jp/2011/05/git.html)
* [ProGit 9. Git の内側](http://progit.org/book/ja/ch9-0.html)
* [Wrangling Git](http://speakerdeck.com/u/schacon/p/wrangling-git)
* [入門 Git](http://www.shuwasystem.co.jp/products/7980html/2380.html) 2章 git の基本概念
* [Git によるバージョン管理](http://ssl.ohmsha.co.jp/cgi-bin/menu.cgi?ISBN=978-4-274-06864-5) 13章 Git リポジトリの中身を見る
* [gitcore-tutorial(7)](http://schacon.github.com/git/gitcore-tutorial.html)
* [git(1): LOW-LEVEL COMMANDS](http://schacon.github.com/git/git.html)

!SLIDE
## We are hiring!!
![gumi](../about_me/gu3.png)では低レベルな技術者を募集しています！

!SLIDE 
# 質疑応答
