!SLIDE
# オブジェクトデータベース

## .git/objects

!SLIDE bullet incremental
## .git/objects の特徴
* 変更(デルタ)ではなくスナップショット
* 各々のコミットに対するツリー構造とデータをまるごと保管する

!SLIDE bullet incremental
## オブジェクトの種類
オブジェクトデータベース(.git/objects)に格納されるオブジェクト

* blob
* tree
* commit
* tag (今回省略します)

!SLIDE
# blob object

!SLIDE
# データそのものを指す<br />オブジェクト

!SLIDE commandline incremental
## オブジェクト ID は SHA-1 ハッシュ

	$ echo 'Hello, World!' > greeting

	$ git hash-object greeting
	8ab686eafeb1f44702738c8b0f24f2567c36da6d

!SLIDE commandline incremental
## blob はファイル名に関係なく<br />中身が同じならば同じ ID

	$ echo 'Hello, World!' > greeting2

	$ git hash-object greeting greeting2
	8ab686eafeb1f44702738c8b0f24f2567c36da6d
	8ab686eafeb1f44702738c8b0f24f2567c36da6d

!SLIDE commandline incremental
## オブジェクトはオブジェクトデータベースに<br/>ファイルで管理される
先頭2桁のディレクトリ名/残り38桁のファイル名

	$ git add greeting

	$ tree .git
	.git # (色々省略)
	├── index # インデックス
	└── objects
	    └─ 8a
          └── b686eafeb1f44702738c8b0f24f2567c36da6d

	$ git cat-file -t 8ab6
	blob

	$ git cat-file blob 8ab6
	Hello, World!

!SLIDE commandline incremental small
## オブジェクトは読み込み権限で作成される
一度作成されたオブジェクトは上書きされないことを示唆している

	$ stat -c %A .git/objects/8a/b686eafeb1f44702738c8b0f24f2567c36da6d
	-r--r--r--

!SLIDE commandline incremental small
## 同じ内容の blob を追加してもオブジェクトは置換されない
更新時刻は変わらないので置換されていないことがわかる

	$ stat -c %y .git/objects/8a/b686eafeb1f44702738c8b0f24f2567c36da6d
	2012-04-23 09:43:12.000000000 +0900

	$ git add greeting2

	$ stat -c %y .git/objects/8a/b686eafeb1f44702738c8b0f24f2567c36da6d
	2012-04-23 09:43:12.000000000 +0900

!SLIDE commandline incremental
## 削除してもオブジェクトデータベースから<br />消えない

	$ git rm --cached greeting greeting2
	rm 'greeting'
	rm 'greeting2'

	$ git cat-file blob 8ab6
	Hello, World!

!SLIDE bullet incremental small
## blob object についてわかったこと
* オブジェクトは SHA-1 ハッシュ ID で一意になる
* blob はデータの中身のみで一意になる
* オブジェクトデータベースは追記のみで更新しない
* 削除コマンドを実行しても実体は残る
* いわゆるイミュータブル(不変)なオブジェクト

!SLIDE
# tree object

!SLIDE
# blob にファイル構造を<br/>与えるオブジェクト

!SLIDE commandline incremental small
## tree はコミット時に作られる

	$ git add greeting

	$ git commit -m 'added my greeting.'
	[master (root-commit) 77d0330] added my greeting.
	 1 file changed,  1 insertion(+)
	   create mode 100644 greeting

	$ git cat-file commit HEAD # 最新コミットの中身をみる
	tree 2da064c4206cb1e94a20a99c2cd2e19f3d193b74
	author Youhei Nitta <me@youhei.jp> 1335212302 +0900
	committer Youhei Nitta <me@youhei.jp> 1335212302 +0900
	
	added my greeting.

	$ git cat-file -t 2da0
	tree

!SLIDE commandline incremental small
## tree は blob や tree を保持している

	$ git ls-tree 2da0
	100644 blob 8ab686eafeb1f44702738c8b0f24f2567c36da6d    greeting

	$ mkdir subdir && mv greeting2

	$ git add subdir

	$ git commit -m 'added sub directory.'

	$ git ls-tree HEAD
	040000 tree 18e6d2abde0f316ff62e0c8093ca8f569910bf7d    subdir
	100644 blob 8ab686eafeb1f44702738c8b0f24f2567c36da6d    greeting

	$ git ls-tree 18e6
	100644 blob 8ab686eafeb1f44702738c8b0f24f2567c36da6d    greeting2

!SLIDE bullet incremental small
## tree object についてわかったこと
* 構造や名前をもたない blob にファイルシステムとしての構造を与える
* blob や tree を保管している
* tree はコミットに保持される

!SLIDE
# commit object

!SLIDE
## ある時点でのスナップショットを<br/>示すオブジェクト

!SLIDE commandline incremental small
## tree のオブジェクト ID を持つ
	$ git cat-file commit HEAD
	tree 680e36390174676a7343ec570f9f22d0632f4444
	parent 77d03308354257e850041fd2d10448fc3a2c4c8b
	author Youhei Nitta <me@youhei.jp> 1335213434 +0900
	committer Youhei Nitta <me@youhei.jp> 1335213434 +0900
	
	added sub directory.

	$ git ls-tree commit 680e
	040000 tree 18e6d2abde0f316ff62e0c8093ca8f569910bf7d    subdir
	100644 blob 8ab686eafeb1f44702738c8b0f24f2567c36da6d    greeting

!SLIDE commandline incremental smaller
## 親コミットのオブジェクト ID を持つ(最初のコミットを除く)
	$ git cat-file commit HEAD
	tree 680e36390174676a7343ec570f9f22d0632f4444
	parent 77d03308354257e850041fd2d10448fc3a2c4c8b
	author Youhei Nitta <me@youhei.jp> 1335213434 +0900
	committer Youhei Nitta <me@youhei.jp> 1335213434 +0900
	
	added sub directory.

	$ git cat-file -t 77d0
	commit

	$ git cat-file commit 77d0
	tree 2da064c4206cb1e94a20a99c2cd2e19f3d193b74
	author Youhei Nitta <me@youhei.jp> 1335212302 +0900
	committer Youhei Nitta <me@youhei.jp> 1335212302 +0900
	
	added my greeting.

!SLIDE commandline incremental small
## マージコミットは二つの親コミットを持つ
(少し高レベルに戻ります)

	$ git branch fukuoka
	$ git checkout fukuoka
	$ echo 'Hello, Fukuoka!' > greeting2
	$ git add greeting2
	$ git commit -m 'added another greeting.'
	$ git checkout master
	$ git merge fukuoka -m 'merged fukuoka branch.'

	$ git cat-file commit HEAD
	tree 2fb79db8e8b4ab0f704a056754b434ff2a5435b9
	parent ae3bc73b86e8ea701496122f4ea7ec5e29cab979
	parent 5d8fc0a8aef3930dac4347bdfda950cec83bde8c
	author Youhei Nitta <me@youhei.jp> 1335215713 +0900
	committer Youhei Nitta <me@youhei.jp> 1335215713 +0900
	
	merged fukuoka branch.

!SLIDE bullet incremental small
## commit object についてわかったこと
* 必ず tree を持っている
* つまりコミット時点でのツリーの<br/>完全な状態(スナップショット)を持っている
* parent を持っている
* マージコミットは parent を二つ持っている
* つまり parent を辿れば「履歴」を構成できる

!SLIDE
# Git の実体(エンティティ)は基本的にはこれだけです
## とてもシンプルです

!SLIDE bullet
## 残りの登場人物はふたつ
* インデックス
* リファレンス
