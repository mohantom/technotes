Git
=======

Git github
Git, gitbash, Cygwin, git service gitolite
Gitbash ~windows  /home/administrator/.ssh/
Cygwin	/home/adminxxxx/.ssh

Ubuntu，工具oh-my-zsh
命令行更强大

Cygwin 1.7

## init
```shell script
mkdir test
cd test/
git init demo4
cd demo4/
ls -lat
cd .git		// 各版本存在这里
```


```shell script
vi a.txt
git add a.txt		//放到提交任务(暂存区)
git status		// 查看任务状态
git commit -m "The first commit"		//必须要加message

git config		// 设置参数 (用户global, system, locale)

git hist		//查看提交记录/标识
```

## commit
```shell script
git add a.txt		//改动不会自动提交, 必须add
git commit -m "comment2"

git commit -a -m "commit3" 		//或者用这个, 但不推荐
git log
```


## diff
```shell script
git diff		// 显示修改差别
git checkout .		// 撤销提交的更改

git diff head		// head就是master (最后一个提交) 工作区和Head
git diff --cached	// 暂存区和head

// 第一个M表示版本库和处理中间状态有差异
// 第二个M表示工作区和当前文件有差异
```


## stash
```shell script
git reset head a.txt		// 从暂存区拿走指定的a.txt 回复到原始状态

git stash		// 保存在 branch做的修改, 切换分支, 但又不想提交
git stash pop	// 找回保存的branch
```


```shell script
git log -pretty=raw -graph 872b140	//显示对象间关系
// Tree, parent, author, committer

git checkout test		// switched to branch 'test'
git branch		// master  * test	(星号表示当前分支)

pringf git |shalsum	//保证全球唯一
```


## Reset
```shell script
git reset
git reflog

// 撤销修改
// 如果修改某一个文件(没有git add, 已被提交过), 想撤销这次修改(确定没任何用处)?
git checkout a.txt		// 或者目录 /src/ (比较危险)

// 如果已修改几个文件, 但是想撤销到某个版本, 但是当前暂存区, 工作区不想撤销?
git reset --soft commiID

// 如果已修改几个文件也提交了暂存区了, 想撤销到某个commit(起始还可以找回)
git reset --hard commiID

// 取消撤销
git reflog show master		// 显示 master 历史版本(最下面的最新 master@{2})
git reset -hard master@{1}
```



## checkout
```shell script
git push origin master
cat gitcheckout.txt	// 查看文件, 显示其内容

cat ../.git/HEAD	
git branch -v
git reflog -1
vim gitchina.org		//编辑
git merge commitID
git cat-file -p HEAD

// 分离头指针
cat .git/head
git branch
git checkout
git reflog

// 挽救分离头指针
git checkout .		// 当前目录
git checkout fileName
git checkout directoryName


// Git stash实际用的不多

git reset --soft head^
git reset--sof^C

// 主要用下面两个命令
git stash		// 保存branch
git stash pop	// 找回branch
```


