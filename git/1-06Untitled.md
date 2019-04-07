cat命令主要用来查看文件内容，创建文件，文件合并，追加文件内容等功能。

cat HEAD 查看HEAD文件的内容  
git cat-file 命令 显示版本库对象的内容、类型及大小信息。
git cat-file -t b44dd71d62a5a8ed3 显示版本库对象的类型
git cat-file -s b44dd71d62a5a8ed3 显示版本库对象的大小
git cat-file -p b44dd71d62a5a8ed3 显示版本库对象的内容

HEAD：指向当前的工作路径
config：存放本地仓库（local）相关的配置信息。
refs/heads:存放分支
refs/tags:存放tag，又叫里程牌 （当这次commit是具有里程碑意义的 比如项目1.0的时候 就可以打tag）
objects：存放对象 .git/objects/ 文件夹中的子文件夹都是以哈希值的前两位字符命名 每个object由40位字符组成，前两位字符用来当文件夹，后38位做文件。



git branch -d branch_name:使用-d 在删除前Git会判断在该分支上开发的功能是否被merge的其它分支。如果没有，不能删除。如果merge到其它分支，但之后又在其上做了开发，使用-d还是不能删除。-D会强制删除。

git commit --amend 命令应该是代替（或这说修改）上一次提交，不只是修改message。
比如上一次提交时有几个文件没有add以及commit，可以重新进行add之后再commit --amend提交。
但这次提交之后不会增加一次新的commit，而是相当于在上一次commit的基础上进行修改。

