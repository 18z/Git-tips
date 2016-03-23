## Git-tips

>下面所提到的情境與解法，更詳細的內容可參考：

[Practical guide for git users](http://git-tutorial.readthedocs.org/en/latest/)

>情境一：

```bash
從 Github 上 Clone 一 project 下來後
在此 project 中，開新 branch
將新 branch push 上 Github	

解法： 

1. git clone https://github.com/deanboole/test.git 
2. git checkout -b (new_branch_name) 
3. git push -u origin (new_branch_name)
```

>情境二：

```bash
快速套用各種設定檔 (.vimrc, .gitconfig .bashrc)
須搭配 https://github.com/deanboole/Provision 使用

解法：

git clone Provision 下來後
依照喜好，可開不同 branch 並將設定檔做不同調整

假設現有macos1, macos2兩個 branch
其 .vimrc, .gitconfig, .bashrc 等設定皆不相同
則可使用 git checkout 
切換到不同branch 迅速套用不同設定
```

>情境三：

```bash
Github：
		Commit A (2015/1/1)
		Commit B (2015/1/2)
		Commit C (2015/1/3)

Local：
		Commit A (2015/1/1)
		Commit B (2015/1/2)

Local 編輯前忘記先下 git pull 與Github同步
此時，若下git pull 則會產生錯誤或衝突

解法：

使用git stash
將修改過的地方，先儲存起來
之後再下 git pull
與 Github 同步後
再下 git stash apply，將變更處套用回來
```

>情境四：

```bash
Issue 解完
想在 Commit message 上做超連結

解法：

git commit -m "title" -m "message body"

title 部分可寫成 fixed #6
也就是把第六個 Issue 解掉的意思
```

>情境五：

```bash
發 Pull Request 給其他Project

解法：

1. fork 該 Project
2. git clone 自己 Github 上那份 fork 到 local 端
3. 在 local 端進行修改
4. git push 到自己 Github 上那份 fork
5. 在自己 Github 上按下 open pull Request
```

>情境六：

```bash
更新 fork repository

解法：

1. 在 local 端設定 upstream
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git 

2. git fetch upstream
3. git checkout master
4. git merge upstream/master
```

>情境七：

```bash
備份 github 上面所有 repository

解法：
$ curl "https://raw.github.com/ptrofimov/github-backup-sh/master/github-backup.sh" | sh -s <username>
```

>情境八：

```bash
commit 前，檢查是否以特定 email 提交

1. 在 .gitconfig 裡面至少填入這些資訊

[user]
    email = xxx@gmail.com

[init]
    templatedir = ~/.git/templates


2. vim .git/templates/hooks/pre-commit

填入以下腳本

#!/bin/bash

remote=$(git remote -v |grep push |grep -o "github")
email=$(git config user.email)

if [ $remote == "github" ] && [ $email == "xxx@gmail.com" ]; then
    echo "change your email!"
    exit 1
else
    echo "okay to commit"
    exit 0
fi

3. chmod +x .git/templates/hooks/pre-commit
```

>情境九：

```bash
remote repository 上有多個 branch，想 clone 單一 branch

解法：

1. $ git clone git://example.com/myproject
2. $ cd myproject
3. $ git branch -a
	* master
	remotes/origin/HEAD
	remotes/origin/master
	remotes/origin/v1.0-stable
	remotes/origin/experimental
4. $ git checkout origin/experimental (單純看看內容)
5. $ git checkout -b experimental origin/experimental (clone 下來開發)

```
> 情境十：

```bash
修改前一次 commit 使用者名稱與email

解法：
$ git commit --amend --author "New Author Name <email@address.com>" 
```

> 情境十一：

```bash
將其他 branch 上的 commit pick 來用 (cherry-pick)
假設使用者當前在 development branch，想要 pick hotfix branch 上的 A commit 來用

解法：
$ git cherry-pick A
```

> 情境十二：

```bash
重新命名 local branch 與 remote branch

解法：
$ git branch -m old_branch new_branch         # Rename branch locally    
$ git push origin :old_branch                 # Delete the old branch    
$ git push --set-upstream origin new_branch   # Push the new branch, set local branch to track the new remote
```

> Git 答問區：

問：git pull 跟 git fetch 差別？

答：git pull = git fetch + git merge
