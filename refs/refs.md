!SLIDE 
# リファレンス

## .git/refs

!SLIDE bullet incremental small
## リファレンスとは
* 覚えにくいオブジェクト ID の代わりに使う別名
* ローカルブランチ, リモートブランチ, タグ, HEAD は全てリファレンス

!SLIDE bullet incremental
## リファレンスの種類
* references
* symbolic references
* remote references (今回省略します)

!SLIDE commandline incremental smaller
## branch は references

	$ cat .git/refs/heads/master
	41219f49d28b936482be893a6ca3b5a77443c78a

	$ git cat-file commit master
	tree 2fb79db8e8b4ab0f704a056754b434ff2a5435b9
	parent ae3bc73b86e8ea701496122f4ea7ec5e29cab979
	parent 5d8fc0a8aef3930dac4347bdfda950cec83bde8c
	author Youhei Nitta <me@youhei.jp> 1335215713 +0900
	committer Youhei Nitta <me@youhei.jp> 1335215713 +0900
	
	Merge branch 'fukuoka'

	$ git cat-file commit 41219f49d28b936482be893a6ca3b5a77443c78a
	tree 2fb79db8e8b4ab0f704a056754b434ff2a5435b9
	parent ae3bc73b86e8ea701496122f4ea7ec5e29cab979
	parent 5d8fc0a8aef3930dac4347bdfda950cec83bde8c
	author Youhei Nitta <me@youhei.jp> 1335215713 +0900
	committer Youhei Nitta <me@youhei.jp> 1335215713 +0900
	
	Merge branch 'fukuoka'

!SLIDE commandline incremental smaller
## HEAD は symbolic references
他の references へのポインタで表現されている

	$ cat .git/refs/HEAD
	ref: refs/heads/master

	$ git symbolic-ref HEAD
	refs/heads/master

	$ git cat-file commit HEAD
	tree 2fb79db8e8b4ab0f704a056754b434ff2a5435b9
	parent ae3bc73b86e8ea701496122f4ea7ec5e29cab979
	parent 5d8fc0a8aef3930dac4347bdfda950cec83bde8c
	author Youhei Nitta <me@youhei.jp> 1335215713 +0900
	committer Youhei Nitta <me@youhei.jp> 1335215713 +0900
	
	Merge branch 'fukuoka'

!SLIDE commandline incremental smaller
## tag も references

	$ git tag v0.0.1

	$ cat .git/refs/tags/v0.0.1
	41219f49d28b936482be893a6ca3b5a77443c78a

	$ git cat-file commit v0.0.1
	tree 2fb79db8e8b4ab0f704a056754b434ff2a5435b9
	parent ae3bc73b86e8ea701496122f4ea7ec5e29cab979
	parent 5d8fc0a8aef3930dac4347bdfda950cec83bde8c
	author Youhei Nitta <me@youhei.jp> 1335215713 +0900
	committer Youhei Nitta <me@youhei.jp> 1335215713 +0900
	
	Merge branch 'fukuoka'

	$ git cat-file commit 41219f49d28b936482be893a6ca3b5a77443c78a
	tree 2fb79db8e8b4ab0f704a056754b434ff2a5435b9
	parent ae3bc73b86e8ea701496122f4ea7ec5e29cab979
	parent 5d8fc0a8aef3930dac4347bdfda950cec83bde8c
	author Youhei Nitta <me@youhei.jp> 1335215713 +0900
	committer Youhei Nitta <me@youhei.jp> 1335215713 +0900
	
	Merge branch 'fukuoka'

!SLIDE bullet incremental
## tag と branch の違い
* 実はほとんど同じ
* branch は commit に合わせて変動する
* 逆に tag は変動しない branch といえる
