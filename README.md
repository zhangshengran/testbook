#gitbook

##git使用总结

**1.版本回退**
-- HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。

-- 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

-- 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

**2.工作区和暂存区**

![Alt](./images/0.jpg)

**3.管理修改**

git add填加到暂存区,git commit 添加到版本库

**4.撤销修改**

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，版本回退，使用命令git reset --hard commit_id

**5.分支管理**


查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>



WINDOWS AD
testVIM
shell test
