!SLIDE
# みなさん Git 使ってますか?

!SLIDE
# Git ってなんかわかりにくくないですか？

!SLIDE
# 自分はわかりにくいなあと感じていました

!SLIDE
# はてブ, Twitter に溢れる<br/>初心者向け Tips

!SLIDE
# 各地で開催される<br/>Git 勉強会

!SLIDE
# Git のわかりにくさを解消するための様々なツール

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

!SLIDE commandline small
## [git-flow](https://github.com/nvie/gitflow)

	$ git flow init
	$ git flow feature start branch_name
	$ git flow feature end branch_name
	$ git flow hotfix
	$ git flow release

!SLIDE commandline small
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

!SLIDE bullet incremental small
# 「本質的な理解」に近付くには
* 高レベルの抽象化されたコマンドやオプションを使いこなせても Git がわかった感じがしない
* 対症療法的な解決になりがち
* ググってコマンド打ってみる、とか
* それは Git の内部を理解していないから
* しかしコマンドやオプションは全て理解するには数がとても多い
* データに焦点を当てると覚えることが少なそう

!SLIDE
# と、いうことでデータ構造の観点から Git を調べてみました

!SLIDE bullet small
# Git を実践的に使う上で欠かせない高レベルな機能
* 分散リポジトリ
* add --patch
* merge, pull --rebase
* stash, reflog
* rebase -i による歴史の改変

!SLIDE bullet small
# これらはこのスライドのスコープ外です
* 一旦お忘れください
* (実践 Git と言っておきながら...)
