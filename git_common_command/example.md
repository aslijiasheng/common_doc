git reset命令演示
demonstrate below
--hard
# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:01:15]
$ echo "doc3.md" >> doc3.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:01:29]
$ g add doc3.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:01:34]
$ echo "changed doc2.md" >> doc2.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:01:49]
$ g st
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   doc3.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   doc2.md
# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:02:30]
$ git reset --hard
HEAD is now at efe68cb Merge branch 'dev_bfc0c90'

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [13:05:55]
$ g st
On branch master
nothing to commit, working tree clean

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [13:06:17]
$ git ls-files -s
100644 bc52795ce3101b170ab5203c0a4dd5b5566cab49 0	README.md
100644 e55cef116b706eddcb180bf59421fbf8695f4f94 0	doc.md
100644 0ee9be4bc1aba6e9ae0f83a6673c46390165afb2 0	doc1.md
100644 03d1839ece23cc847802e3ef0993cffeffaf36fd 0	doc2.md

--hard会直接删除工作空间改动代码，撤销commit，撤销 git add .

--mixed
# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:22:19]
$ echo 'new file content' > doc3.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:22:40]
$ g add doc3.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:22:46]
$ echo 'append content' >> doc2.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:22:58]
$ g add doc2.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:23:02]
$ g st
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   doc2.md
	new file:   doc3.md


# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:23:05]
$ git ls-files -s
100644 bc52795ce3101b170ab5203c0a4dd5b5566cab49 0	README.md
100644 e55cef116b706eddcb180bf59421fbf8695f4f94 0	doc.md
100644 0ee9be4bc1aba6e9ae0f83a6673c46390165afb2 0	doc1.md
100644 88c3d5fa0ec1ca95657a30326198bba462a6825e 0	doc2.md
100644 8e66654a5477b1bf4765946147c49509a431f963 0	doc3.md
# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:23:11]
$ g reset --mixed
Unstaged changes after reset:
M	doc2.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:23:36]
$ g st
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   doc2.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	doc3.md

no changes added to commit (use "git add" and/or "git commit -a")
--mixed 不删除工作空间改动代码，撤销commit，并且撤销 git add . 操作
--soft
# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [13:26:41]
$ echo 'append content' >> doc2.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:27:10]
$ g add doc2.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:27:14]
$ git ls-files -s
100644 bc52795ce3101b170ab5203c0a4dd5b5566cab49 0	README.md
100644 e55cef116b706eddcb180bf59421fbf8695f4f94 0	doc.md
100644 0ee9be4bc1aba6e9ae0f83a6673c46390165afb2 0	doc1.md
100644 88c3d5fa0ec1ca95657a30326198bba462a6825e 0	doc2.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:27:38]
$ g st
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   doc2.md


# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:27:52]
$ git reset --soft

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:28:03]
$ g st
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   doc2.md


# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:28:05]
$ git ls-files -s
100644 bc52795ce3101b170ab5203c0a4dd5b5566cab49 0	README.md
100644 e55cef116b706eddcb180bf59421fbf8695f4f94 0	doc.md
100644 0ee9be4bc1aba6e9ae0f83a6673c46390165afb2 0	doc1.md
100644 88c3d5fa0ec1ca95657a30326198bba462a6825e 0	doc2.md
--soft 不删除工作空间改动代码，撤销commit，不撤销 git add
remote: Resolving deltas: 100% (1/1), completed with 1 local object.

* ce025a8 - (HEAD -> master) doc4.md (1 second ago) <jason>
* cedafc6 - doc3.md (11 seconds ago) <jason>
* 3cc949d - (origin/master) doc2.md (2 minutes ago) <jason>
*   efe68cb - Merge branch 'dev_bfc0c90' (15 hours ago) <sky>
|\
| * 60d6fd2 - (dev_bfc0c90) doc1.md (15 hours ago) <sky>
* | 29135e3 - (dev) dev commit (16 hours ago) <sky>
* | c7aad2f - doc1.md (16 hours ago) <sky>
* | 8e04fef - 批量提交 (16 hours ago) <sky>
|/
* bfc0c90 - again add doc.md (16 hours ago) <sky>
* 7a6e289 - Initial commit (16 hours ago) <jason>
现在要回滚到cedafc6提交记录
* cedafc6 - (HEAD -> master) doc3.md (9 minutes ago) <jason>
* 3cc949d - (origin/master) doc2.md (10 minutes ago) <jason>
*   efe68cb - Merge branch 'dev_bfc0c90' (16 hours ago) <sky>
|\
| * 60d6fd2 - (dev_bfc0c90) doc1.md (16 hours ago) <sky>
* | 29135e3 - (dev) dev commit (16 hours ago) <sky>
* | c7aad2f - doc1.md (16 hours ago) <sky>
* | 8e04fef - 批量提交 (16 hours ago) <sky>
|/
* bfc0c90 - again add doc.md (16 hours ago) <sky>
* 7a6e289 - Initial commit (17 hours ago) <jason>
ce025a8 提交记录没了并且回滚成功到cedafc6提交记录
----------------------------------------------------
git revert命令演示
# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [13:44:44]
$ touch revert.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:46:21]
$ echo "revert.md" >> revert.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:46:30]
$ echo "update doc4.md" >> doc4.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:47:51]
$ g co -- doc4.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:48:11]
$ g st
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	revert.md

nothing added to commit but untracked files present (use "git add" to track)

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:48:13]
$ g commit -m 'revert.md'
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	revert.md

nothing added to commit but untracked files present (use "git add" to track)

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:48:23] C:1
$ g add revert.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:48:34]
$ g commit -m 'revert.md'
[master e9f054f] revert.md
 1 file changed, 1 insertion(+)
 create mode 100644 revert.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [13:48:43]
$ echo "modified doc3.md" >> doc3.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:49:00]
$ g add doc3.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [13:49:11]
$ g commit -m 'modified doc3.md'
[master 785d5fc] modified doc3.md
 1 file changed, 1 insertion(+)

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [13:49:29]
$ g lg
* 785d5fc - (HEAD -> master) modified doc3.md (5 seconds ago) <jason>
* e9f054f - revert.md (51 seconds ago) <jason>
* f36dd87 - (origin/master) doc4.md (5 minutes ago) <jason>
* cedafc6 - doc3.md (17 minutes ago) <jason>
* 3cc949d - doc2.md (19 minutes ago) <jason>
*   efe68cb - Merge branch 'dev_bfc0c90' (16 hours ago) <sky>
|\
| * 60d6fd2 - (dev_bfc0c90) doc1.md (16 hours ago) <sky>
* | 29135e3 - (dev) dev commit (16 hours ago) <sky>
* | c7aad2f - doc1.md (16 hours ago) <sky>
* | 8e04fef - 批量提交 (16 hours ago) <sky>
|/
* bfc0c90 - again add doc.md (16 hours ago) <sky>
* 7a6e289 - Initial commit (17 hours ago) <jason>
现在我们需要撤销e9f054f这次提交记录
git revert e9f054f
* f0a9406 - (HEAD -> master) Revert "commit revert1.md" (2 minutes ago) <jason>
* 8303935 - commit revert1.md (2 minutes ago) <jason>
* df5137b - commit revert.md (3 minutes ago) <jason>
* fc6951a - Revert "revert.md" (6 minutes ago) <jason>
* 785d5fc - modified doc3.md (7 minutes ago) <jason>
* e9f054f - revert.md (8 minutes ago) <jason>
* f36dd87 - (origin/master) doc4.md (12 minutes ago) <jason>
* cedafc6 - doc3.md (24 minutes ago) <jason>
* 3cc949d - doc2.md (25 minutes ago) <jason>
*   efe68cb - Merge branch 'dev_bfc0c90' (16 hours ago) <sky>
|\
| * 60d6fd2 - (dev_bfc0c90) doc1.md (16 hours ago) <sky>
* | 29135e3 - (dev) dev commit (16 hours ago) <sky>
* | c7aad2f - doc1.md (16 hours ago) <sky>
* | 8e04fef - 批量提交 (16 hours ago) <sky>
|/
* bfc0c90 - again add doc.md (16 hours ago) <sky>
* 7a6e289 - Initial commit (17 hours ago) <jason>
可以发现revert的撤销操作是在当前commit下又追加了一个新的commit，而且revert会保留撤销前后的commit history

git merge命令演示
Fast Forward Merge
master分支没有改动, merge_test分支改动频繁
# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:01:30]
$ g co -b merge_test
Switched to a new branch 'merge_test'

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test o [14:01:39]
$ l
total 48
drwxr-xr-x   9 sky  wheel   288B Apr  6 14:01 .
drwxr-xr-x  37 sky  wheel   1.2K Apr  5 21:14 ..
drwxr-xr-x  14 sky  wheel   448B Apr  6 14:01 .git
-rw-r--r--   1 sky  wheel    13B Apr  5 21:16 README.md
-rw-r--r--   1 sky  wheel    69B Apr  5 22:32 doc.md
-rw-r--r--   1 sky  wheel    11B Apr  5 22:03 doc1.md
-rw-r--r--   1 sky  wheel    25B Apr  6 14:01 doc2.md
-rw-r--r--   1 sky  wheel    25B Apr  6 14:01 doc3.md
-rw-r--r--   1 sky  wheel     8B Apr  6 14:01 doc4.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test o [14:01:42]
$ touch merge_test.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:03:23]
$ echo "merge_test" >> merge_test.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:03:32]
$ touch merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:03:44]
$ echo "merge_test1" >> merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:03:54]
$ g commit -am 'commit merge_test md'
On branch merge_test
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	merge_test.md
	merge_test1.md

nothing added to commit but untracked files present (use "git add" to track)

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:04:09] C:1
$ g add merge_test.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:04:38]
$ g commit -m 'commit merge_test md'
[merge_test c91c256] commit merge_test md
 1 file changed, 1 insertion(+)
 create mode 100644 merge_test.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:04:48]
$ g add merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:04:53]
$ g commit -m 'commit merge_test1 md'
[merge_test 80b1efe] commit merge_test1 md
 1 file changed, 1 insertion(+)
 create mode 100644 merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test o [14:04:57]
$ l
total 64
drwxr-xr-x  11 sky  wheel   352B Apr  6 14:03 .
drwxr-xr-x  37 sky  wheel   1.2K Apr  5 21:14 ..
drwxr-xr-x  14 sky  wheel   448B Apr  6 14:04 .git
-rw-r--r--   1 sky  wheel    13B Apr  5 21:16 README.md
-rw-r--r--   1 sky  wheel    69B Apr  5 22:32 doc.md
-rw-r--r--   1 sky  wheel    11B Apr  5 22:03 doc1.md
-rw-r--r--   1 sky  wheel    25B Apr  6 14:01 doc2.md
-rw-r--r--   1 sky  wheel    25B Apr  6 14:01 doc3.md
-rw-r--r--   1 sky  wheel     8B Apr  6 14:01 doc4.md
-rw-r--r--   1 sky  wheel    11B Apr  6 14:03 merge_test.md
-rw-r--r--   1 sky  wheel    12B Apr  6 14:03 merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test o [14:05:04]
$ g co master
Switched to branch 'master'

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:05:08]
$ g lg

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:05:20]
$ g merge merge_test
Updating 28fd724..80b1efe
Fast-forward
 merge_test.md  | 1 +
 merge_test1.md | 1 +
 2 files changed, 2 insertions(+)
 create mode 100644 merge_test.md
 create mode 100644 merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:05:33]
$ l
total 64
drwxr-xr-x  11 sky  wheel   352B Apr  6 14:05 .
drwxr-xr-x  37 sky  wheel   1.2K Apr  5 21:14 ..
drwxr-xr-x  14 sky  wheel   448B Apr  6 14:05 .git
-rw-r--r--   1 sky  wheel    13B Apr  5 21:16 README.md
-rw-r--r--   1 sky  wheel    69B Apr  5 22:32 doc.md
-rw-r--r--   1 sky  wheel    11B Apr  5 22:03 doc1.md
-rw-r--r--   1 sky  wheel    25B Apr  6 14:01 doc2.md
-rw-r--r--   1 sky  wheel    25B Apr  6 14:01 doc3.md
-rw-r--r--   1 sky  wheel     8B Apr  6 14:01 doc4.md
-rw-r--r--   1 sky  wheel    11B Apr  6 14:05 merge_test.md
-rw-r--r--   1 sky  wheel    12B Apr  6 14:05 merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:05:38]
$ g lg
未合并前的log
* 28fd724 - (HEAD -> master, origin/master) commit revert.md (5 minutes ago) <jason>
* f0a9406 - Revert "commit revert1.md" (11 minutes ago) <jason>
* 8303935 - commit revert1.md (11 minutes ago) <jason>
* df5137b - commit revert.md (11 minutes ago) <jason>
* fc6951a - Revert "revert.md" (15 minutes ago) <jason>
* 785d5fc - modified doc3.md (16 minutes ago) <jason>
* e9f054f - revert.md (17 minutes ago) <jason>
* f36dd87 - doc4.md (21 minutes ago) <jason>
* cedafc6 - doc3.md (33 minutes ago) <jason>
* 3cc949d - doc2.md (34 minutes ago) <jason>
*   efe68cb - Merge branch 'dev_bfc0c90' (16 hours ago) <sky>
|\
| * 60d6fd2 - (dev_bfc0c90) doc1.md (16 hours ago) <sky>
* | 29135e3 - (dev) dev commit (16 hours ago) <sky>
* | c7aad2f - doc1.md (16 hours ago) <sky>
* | 8e04fef - 批量提交 (16 hours ago) <sky>
|/
* bfc0c90 - again add doc.md (17 hours ago) <sky>
* 7a6e289 - Initial commit (17 hours ago) <jason>
合并后的log
* 80b1efe - (HEAD -> master, merge_test) commit merge_test1 md (43 seconds ago) <jason>
* c91c256 - commit merge_test md (52 seconds ago) <jason>
* 28fd724 - (origin/master) commit revert.md (5 minutes ago) <jason>
* f0a9406 - Revert "commit revert1.md" (11 minutes ago) <jason>
* 8303935 - commit revert1.md (11 minutes ago) <jason>
* df5137b - commit revert.md (12 minutes ago) <jason>
* fc6951a - Revert "revert.md" (15 minutes ago) <jason>
* 785d5fc - modified doc3.md (16 minutes ago) <jason>
* e9f054f - revert.md (17 minutes ago) <jason>
* f36dd87 - doc4.md (21 minutes ago) <jason>
* cedafc6 - doc3.md (33 minutes ago) <jason>
* 3cc949d - doc2.md (35 minutes ago) <jason>
*   efe68cb - Merge branch 'dev_bfc0c90' (16 hours ago) <sky>
|\
| * 60d6fd2 - (dev_bfc0c90) doc1.md (16 hours ago) <sky>
* | 29135e3 - (dev) dev commit (16 hours ago) <sky>
* | c7aad2f - doc1.md (16 hours ago) <sky>
* | 8e04fef - 批量提交 (16 hours ago) <sky>
|/
* bfc0c90 - again add doc.md (17 hours ago) <sky>
* 7a6e289 - Initial commit (17 hours ago) <jason>
--no--off演示
*   cc076c2 - (HEAD -> master) Merge branch 'merge_test' (4 seconds ago) <jason>
|\
| * 859267e - (merge_test) update commit merge_nooff_test md (11 seconds ago) <jason>
|/
* 66507c1 - commit merge_nooff_test md (85 seconds ago) <jason>
* 80b1efe - commit merge_test1 md (5 minutes ago) <jason>
* c91c256 - commit merge_test md (5 minutes ago) <jason>
* 28fd724 - (origin/master) commit revert.md (9 minutes ago) <jason>
* f0a9406 - Revert "commit revert1.md" (15 minutes ago) <jason>
* 8303935 - commit revert1.md (15 minutes ago) <jason>
* df5137b - commit revert.md (16 minutes ago) <jason>
* fc6951a - Revert "revert.md" (19 minutes ago) <jason>
* 785d5fc - modified doc3.md (20 minutes ago) <jason>
* e9f054f - revert.md (21 minutes ago) <jason>
* f36dd87 - doc4.md (25 minutes ago) <jason>
* cedafc6 - doc3.md (37 minutes ago) <jason>
* 3cc949d - doc2.md (39 minutes ago) <jason>
*   efe68cb - Merge branch 'dev_bfc0c90' (16 hours ago) <sky>
|\
| * 60d6fd2 - (dev_bfc0c90) doc1.md (16 hours ago) <sky>
* | 29135e3 - (dev) dev commit (16 hours ago) <sky>
* | c7aad2f - doc1.md (17 hours ago) <sky>
* | 8e04fef - 批量提交 (17 hours ago) <sky>
|/
* bfc0c90 - again add doc.md (17 hours ago) <sky>
* 7a6e289 - Initial commit (17 hours ago) <jason>
3-way merge演示
master有变动 merge_test分支也有变动
# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:10:01]
$ g co merge_test
Switched to branch 'merge_test'

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test o [14:11:30]
$ l
total 72
drwxr-xr-x  12 sky  wheel   384B Apr  6 14:09 .
drwxr-xr-x  37 sky  wheel   1.2K Apr  5 21:14 ..
drwxr-xr-x  14 sky  wheel   448B Apr  6 14:11 .git
-rw-r--r--   1 sky  wheel    13B Apr  5 21:16 README.md
-rw-r--r--   1 sky  wheel    69B Apr  5 22:32 doc.md
-rw-r--r--   1 sky  wheel    11B Apr  5 22:03 doc1.md
-rw-r--r--   1 sky  wheel    25B Apr  6 14:01 doc2.md
-rw-r--r--   1 sky  wheel    25B Apr  6 14:01 doc3.md
-rw-r--r--   1 sky  wheel     8B Apr  6 14:01 doc4.md
-rw-r--r--   1 sky  wheel    25B Apr  6 14:09 merge_nooff_test.md
-rw-r--r--   1 sky  wheel    11B Apr  6 14:05 merge_test.md
-rw-r--r--   1 sky  wheel    12B Apr  6 14:05 merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test o [14:11:30]
$ touch 3_way_merge.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:11:38]
$ echo "3-way" >> 3_way_merge.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:11:45]
$ g add 3_way_merge.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:11:49]
$ g commit -m 'commit 3_way_merge md'
[merge_test e6aa95b] commit 3_way_merge md
 1 file changed, 1 insertion(+)
 create mode 100644 3_way_merge.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test o [14:12:00]
$ g co master
Switched to branch 'master'

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:12:30]
$ touch doc5.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [14:12:34]
$ echo "doc5.md" >> doc5.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [14:12:42]
$ g add doc5.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [14:12:47]
$ g commit -m 'commit doc5 md'
[master 8a3c4ee] commit doc5 md
 1 file changed, 1 insertion(+)
 create mode 100644 doc5.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:12:53]
$ g merge merge_test
Merge made by the 'recursive' strategy.
 3_way_merge.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 3_way_merge.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:13:11]
$ g lg
*   1a1a1c9 - (HEAD -> master) Merge branch 'merge_test' (2 minutes ago) <jason>
|\
| * e6aa95b - (merge_test) commit 3_way_merge md (3 minutes ago) <jason>
* | 8a3c4ee - commit doc5 md (2 minutes ago) <jason>
* | cc076c2 - Merge branch 'merge_test' (5 minutes ago) <jason>
|\|
| * 859267e - update commit merge_nooff_test md (5 minutes ago) <jason>
|/
* 66507c1 - commit merge_nooff_test md (6 minutes ago) <jason>
* 80b1efe - commit merge_test1 md (10 minutes ago) <jason>
* c91c256 - commit merge_test md (10 minutes ago) <jason>
* 28fd724 - (origin/master) commit revert.md (14 minutes ago) <jason>
* f0a9406 - Revert "commit revert1.md" (20 minutes ago) <jason>
* 8303935 - commit revert1.md (20 minutes ago) <jason>
* df5137b - commit revert.md (21 minutes ago) <jason>
* fc6951a - Revert "revert.md" (24 minutes ago) <jason>
* 785d5fc - modified doc3.md (25 minutes ago) <jason>
* e9f054f - revert.md (26 minutes ago) <jason>
* f36dd87 - doc4.md (30 minutes ago) <jason>
* cedafc6 - doc3.md (42 minutes ago) <jason>
* 3cc949d - doc2.md (44 minutes ago) <jason>
*   efe68cb - Merge branch 'dev_bfc0c90' (16 hours ago) <sky>
|\
| * 60d6fd2 - (dev_bfc0c90) doc1.md (16 hours ago) <sky>
* | 29135e3 - (dev) dev commit (16 hours ago) <sky>
* | c7aad2f - doc1.md (17 hours ago) <sky>
* | 8e04fef - 批量提交 (17 hours ago) <sky>
|/
* bfc0c90 - again add doc.md (17 hours ago) <sky>
* 7a6e289 - Initial commit (17 hours ago) <jason>

如何解决冲突演示
$ g co merge_test
Switched to branch 'merge_test'

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test o [14:15:26]
$ v merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:15:47]
$ g add merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test x [14:15:52]
$ g commit -m 'make conflict md'
[merge_test 4c1dbed] make conflict md
 1 file changed, 1 insertion(+), 1 deletion(-)

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:merge_test o [14:16:03]
$ g co master
Switched to branch 'master'

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:16:06]
$ v merge_test

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:16:12]
$ v merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [14:16:24]
$ g add merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [14:16:39]
$ g merge merge_test
error: Your local changes to the following files would be overwritten by merge:
  merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [14:16:46] C:128
$ g commit -m 'make conflict master md'
[master ef3f8f4] make conflict master md
 1 file changed, 1 insertion(+), 1 deletion(-)

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:17:16]
$ g merge merge_test
Auto-merging merge_test1.md
CONFLICT (content): Merge conflict in merge_test1.md
Automatic merge failed; fix conflicts and then commit the result.

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [14:17:24]
$ v merge_test1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [14:17:55]
$ g st
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   merge_test1.md

no changes added to commit (use "git add" and/or "git commit -a")

git rebase 演示操作
# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:22:16]
$ g co -b rebase_dev
Switched to a new branch 'rebase_dev'

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:rebase_dev o [14:22:39]
$ touch rebase_test.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:rebase_dev x [14:22:52]
$ echo "rebase_test" >> rebase_test.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:rebase_dev x [14:23:01]
$ echo "rebase">> doc5.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:rebase_dev x [14:23:16]
$ g commit -a -m 'Adds new feature rebase'
[rebase_dev b29231d] Adds new feature rebase
 1 file changed, 1 insertion(+)

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:rebase_dev x [14:23:51]
$ g st
On branch rebase_dev
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	rebase_test.md

nothing added to commit but untracked files present (use "git add" to track)

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:rebase_dev x [14:23:54]
$ g add rebase_test.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:rebase_dev x [14:23:59]
$ g commit -a -m 'Add rebase_test'
[rebase_dev fc47011] Add rebase_test
 1 file changed, 1 insertion(+)
 create mode 100644 rebase_test.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:rebase_dev o [14:24:12]
$ g co master
Switched to branch 'master'

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:24:14]
$ g rebase rebase_dev

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:24:28] C:130
$ g lg

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:24:31]
$ g rebase rebase_dev
Successfully rebased and updated refs/heads/master.

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [14:24:37]
$ g lg
* fc47011 - (HEAD -> master, rebase_dev) Add rebase_test (12 minutes ago) <jason>
* b29231d - Adds new feature rebase (13 minutes ago) <jason>
*   f0db97f - (origin/master) make conflict master md (15 minutes ago) <jason>
|\
| * 4c1dbed - (merge_test) make conflict md (21 minutes ago) <jason>
* | ef3f8f4 - make conflict master md (19 minutes ago) <jason>
* | 1a1a1c9 - Merge branch 'merge_test' (23 minutes ago) <jason>
|\|
| * e6aa95b - commit 3_way_merge md (25 minutes ago) <jason>
* | 8a3c4ee - commit doc5 md (24 minutes ago) <jason>
* | cc076c2 - Merge branch 'merge_test' (27 minutes ago) <jason>
|\|
| * 859267e - update commit merge_nooff_test md (27 minutes ago) <jason>
|/
* 66507c1 - commit merge_nooff_test md (28 minutes ago) <jason>
* 80b1efe - commit merge_test1 md (32 minutes ago) <jason>
* c91c256 - commit merge_test md (32 minutes ago) <jason>
* 28fd724 - commit revert.md (36 minutes ago) <jason>
* f0a9406 - Revert "commit revert1.md" (42 minutes ago) <jason>
* 8303935 - commit revert1.md (42 minutes ago) <jason>
* df5137b - commit revert.md (43 minutes ago) <jason>
* fc6951a - Revert "revert.md" (46 minutes ago) <jason>
* 785d5fc - modified doc3.md (47 minutes ago) <jason>
* e9f054f - revert.md (48 minutes ago) <jason>
* f36dd87 - doc4.md (52 minutes ago) <jason>
* cedafc6 - doc3.md (64 minutes ago) <jason>
* 3cc949d - doc2.md (66 minutes ago) <jason>
*   efe68cb - Merge branch 'dev_bfc0c90' (17 hours ago) <sky>
|\
| * 60d6fd2 - (dev_bfc0c90) doc1.md (17 hours ago) <sky>
* | 29135e3 - (dev) dev commit (17 hours ago) <sky>
* | c7aad2f - doc1.md (17 hours ago) <sky>
* | 8e04fef - 批量提交 (17 hours ago) <sky>
|/
* bfc0c90 - again add doc.md (17 hours ago) <sky>
* 7a6e289 - Initial commit (17 hours ago) <jason>

How to undo a git rebase using the reflog demonstrate
# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [15:58:55]
$ mkdir reflog

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [15:59:04]
$ echo "reflog">>reflog/reflog.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [15:59:19]
$ g add .

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [15:59:34]
$ git commit -m "some reflog changes"
[master b8aac33] some reflog changes
 1 file changed, 1 insertion(+)
 create mode 100644 reflog/reflog.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [15:59:50]
$ git log --pretty=oneline

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [15:59:52]
$ echo "reflog1">>reflog/reflog1.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [16:01:31]
$ echo "reflog2">>reflog/reflog2.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [16:01:36]
$ g add .

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master x [16:01:40]
$ g commit -m 'reflog changes md'
[master 5d152fc] reflog changes md
 2 files changed, 2 insertions(+)
 create mode 100644 reflog/reflog1.md
 create mode 100644 reflog/reflog2.md

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [16:01:52]
$ git rebase -i origin/master
Successfully rebased and updated refs/heads/master.

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [16:02:05]
$ git rebase -i origin/master
[detached HEAD b0ad938] some reflog changes
 Date: Mon Apr 6 15:59:42 2020 +0800
 3 files changed, 3 insertions(+)
 create mode 100644 reflog/reflog.md
 create mode 100644 reflog/reflog1.md
 create mode 100644 reflog/reflog2.md
Successfully rebased and updated refs/heads/master.

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [16:02:35]
$ g lg

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [16:02:40]
$ g lg

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [16:02:48]
$ tig

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [16:02:58]
$ g reflog

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [16:03:33]
$ g reset HEAD@{5}

# sky @ skydeMacBook-Pro in /Library/WebServer/Documents/githubpro/git_example on git:master o [16:03:54]
$ tig