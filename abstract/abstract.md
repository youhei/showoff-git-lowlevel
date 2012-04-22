!SLIDE
# みなさん Git 使ってますか?

!SLIDE
# Git ってなんかわかりにくくないですか？

!SLIDE
# 自分はわかりにくいなあと感じました

!SLIDE
# はてブ, Twitter に日々溢れる初心者向け Tips

!SLIDE
# 各地で開催される Git の勉強会

!SLIDE
# (どうやら他の方々も？...)

!SLIDE
# 最近は Git のわかりにくさを解消するための様々なツールがあります

!SLIDE
# GUI

!SLIDE
![sourcetree](sourcetree.png)

[sourcetreeapp.com](http://www.sourcetreeapp.com/)

!SLIDE
![Tower](tower.png)

[git-tower.com](http://www.git-tower.com)

!SLIDE
# CLI

!SLIDE commandline
## [git-flow](https://github.com/nvie/gitflow)

	$ git flow init
	$ git flow feature start branch_name
	$ git flow feature end branch_name

!SLIDE commandline
## [legit](http://www.git-legit.org/) - Git Workflow for Humans

	$ git switch <branch>
	$ git sync
	$ git publish
	$ git unpublish
	$ git harvest
	$ git sprout
	$ git graft
	$ git branches

!SLIDE
# 便利ツールは諸刃の剣
これら高機能なツールは Git を使いやすくしてくれますが、「本質的な理解」をせずとも使えてしまう諸刃の剣でもあります。

!SLIDE bullet incremental
# 「本質的な理解」とはなんだろう？
* 高レベルの抽象化されたコマンドやオプションを使いこなせても Git がわかった感じがしない
* データ構造がわかればわかるのかも

!SLIDE
# と、いうことでデータ構造の観点から Git を調べてみました

!SLIDE
# Git を実践的に使う上で欠かせないキーワードたち
* 分散リポジトリ
* merge, rebase
* 歴史の改変
* これらの理解は今回スコープ外です
* 一旦お忘れください

