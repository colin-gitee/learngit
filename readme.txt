一、初始化git仓库
1、在当前目录新建一个代码库
git init
2、新建一个目录，将其初始化为Git代码库
git init [project-name]
3、下载一个项目和他的整个代码历史
git clone [url]

二、配置
1、全局配置
git config --global user.name "colin"
git config --global user.email "1091586412@qq.com"
git config --global --unset user.email

2、显示git配置
git config --list
3、编辑git配置文件
git config -e

三、增加/删除/修改文件
1、查看状态
git status
2、查看变更内容
git diff



