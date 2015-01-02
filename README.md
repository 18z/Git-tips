## Git-tips

情境一：

		從 Github 上 Clone 一 project 下來後
		在此 project 中，開新 branch
		將新 branch push 上 Github	

解法： 
	
		1. git clone https://github.com/deanboole/test.git 
		2. git checkout -b (new_branch_name) 
		3. git push -u origin (new_branch_name)

情境二：

		快速套用各種設定檔 (.vimrc, .gitconfig .bashrc)
		須搭配 https://github.com/deanboole/Provision 使用

解法：
		
		git clone Provision 下來後
		依照喜好，可開不同 branch 並將設定檔做不同調整
		
		假設現有macos1, macos2兩個 branch
		其 .vimrc, .gitconfig, .bashrc 等設定皆不相同
		則可使用 git checkout 
		切換到不同branch 迅速套用不同設定
