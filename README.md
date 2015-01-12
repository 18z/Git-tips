## Git-tips

>下面所提到的情境與解法，更詳細的內容可參考：

[Practical guide for git users](http://git-tutorial.readthedocs.org/en/latest/)

>情境一：

		從 Github 上 Clone 一 project 下來後
		在此 project 中，開新 branch
		將新 branch push 上 Github	

		解法： 

		1. git clone https://github.com/deanboole/test.git 
		2. git checkout -b (new_branch_name) 
		3. git push -u origin (new_branch_name)

>情境二：

		快速套用各種設定檔 (.vimrc, .gitconfig .bashrc)
		須搭配 https://github.com/deanboole/Provision 使用

		解法：

		git clone Provision 下來後
		依照喜好，可開不同 branch 並將設定檔做不同調整
		
		假設現有macos1, macos2兩個 branch
		其 .vimrc, .gitconfig, .bashrc 等設定皆不相同
		則可使用 git checkout 
		切換到不同branch 迅速套用不同設定

>情境三：

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

>情境四：

		Issue 解完
		想在 Commit message 上做超連結

		解法：

		git commit -m "title" -m "message body"

		title 部分可寫成 fixed #6
		也就是把第六個 Issue 解掉的意思

>情境五：

		發 Pull Request 給其他Project

		解法：

		1. fork 該 Project
		2. git clone 自己 Github 上那份 fork 到 local 端
		3. 在 local 端進行修改
		4. git push 到自己 Github 上那份 fork
		5. 在自己 Github 上按下 open pull Request

>情境六：

		更新 fork repository

		解法：

		1. 在 local 端設定 upstream
		git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git 

		2. git fetch upstream
		3. git checkout master
		4. git merge upstream/master

> Git 答問區：

		問：git pull 跟 git fetch 差別？
		
		答：git pull = git fetch + git merge
		
