## git常用语法
  ur: https://juejin.im/post/6869519303864123399

### 文档查询
#### 展示git命令大纲
  `git help`
  `git --help`
*****
#### 展示git命令大纲全部列表
  `git --help -a`
*****
#### 展示具体命令说明手册
  `git help <xxx>`
*****

### 分支管理规范
#### master分支
  `主分支，用于部署生产环境的分支，确保稳定性`
  `master分支一般由develop分支和hotfix分支合并，任何情况下都不能直接修改代码`
*****
#### test分支
  `测试分支`
*****
#### develop分支
  `开发分支`
*****
#### hotfix
  `修复分支，处理线上紧急bug`
*****

### 差异比较





#### 添加本地分支
  `git branch 分支名`
*****

#### 删除本地分支
  `git branch -D 分支名`
*****

#### 添加远程分支
  `git push origin 分支名`
*****

#### 删除远程分支
  `git push --delete origin 分支名 `
*****

#### 切换本地分支
  `git checkout 分支名`
*****

#### 创建并切换本地分支
  `git checkout -b 分支名`
*****

#### 本地分支和远程分支关联
  `切换到本地分支： git checkout 分子名`  
  `git branch --set-upstream-to origin/远程分支`
*****

#### 合并分支
  `切换到合并的分支： git checkout master`  
  `需要合并的分支： git merge 分支名`  
  `提交： git push`
*****

#### 查询远程分支
  `git branch -r`
*****

#### 查询本地分支和远程分支
  `git branch -a`
*****

#### 查看状态
  `git status`
*****

#### 提交到缓存区
  `git add 文件名`
*****

#### 提交到本地仓库
  `git commit -m "内容"`
*****

#### 提交到远程仓库
  `git push`  
  提交到远程仓库的分支上  
  `git push origin 分支名`
*****

#### 下拉仓库的数据
  `git pull`  
  下拉远程仓库分支的数据  
  `git pull origin 分支名`
*****

#### 提交到本地仓库
  `git commit -m "内容"`
*****

#### 清除
  `clear`
*****

#### git 将仓库的所有分支切换到新的仓库
  `git clone --mirror 旧的仓库地址`
  `cd ***.git `切换到旧仓库的git文件
  `git remote set-url origin 新的仓库地址`
  `git push -f origin`
*****

https://juejin.im/post/6869519303864123399
