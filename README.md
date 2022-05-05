# gitflow
测试 [gitflow](https://github.com/nvie/gitflow) 流程  

### 首先创建一个远程仓库克隆到本地  
```bash
git clone git@github.com:kekoyo/gitflow.git
cd gitflow
```

### 初始化 git flow 工作流  
```bash
git flow init -d #-d 表示 default
```
可以得到一个 `main` 和 `develop` 两个本地分支  

```bash
* develop
  main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
```
并且会自动切换到 `develop` 分支
```bash
git push -u origin develop #先 push 一次 develop 分支
```
然后创建一个 `feature` 功能分支  

```bash
git flow feature start edit-readme
```
会自动进行跳转，然后使用 `vim` 编辑 `README.md` 文件  
最后进行 `add & commit` 操作  
然后 `push` 到远程仓库进行 `pull requests` 及代码审查  

```bash
git add README.md
git commit -m "编辑 README.md 文件"
git push origin feature/edit-readme
```
在 github 确保提交的 pull requests 没有问题后合并到远程的 develop 分支  
然后本地的 develop 分支要进行同步  
```bash
git checkout develop 
git pull #同步远程更新
```
> 如果每次 Pull Requests 时都要切换成 develop 分支，那么可以直接在仓库设置中将 develop 分支设置为默认分支  
  
### develop 分支下创建 release 版本号
```bash
git flow release start '1.0.0'
git flow release finish '1.0.0' #执行该命令时会弹出文件编辑，将版本号前的注释去掉，冒号 wq 保存退出
```
这个过程会修改两次版本号文件，一次是合并到 main 分支，一次是合并到 develop 分支  
最后命令结束可能会进入 main 分支  
```bash
git tag #查看标签版本
```
将 develop 分支更新到远程仓库
```bash
git checkout develop
git push origin develop
```
最后提交 main 分支的 tag 标签  
```bash
git checkout main
git push --tags
```
### hotfix 分支修复 tag
hotfix 是紧急 bug 修复分支。只用于当前发布版本中出现 BUG 和漏洞，无法等到下一个版本时才会使用  
hotfix 分支以 main 分支为起点，不影响 develop 分支的开发情况下创建  
```bash
git checkout main
git fetch origin #从远程获取标签信息（如果这个 tag 是其他人创建的话）
git flow hotfix start '1.0.1' #fix 操作在版本号最后一位数上 +1
```
执行命令之后会自动创建并进入这个 hotfix/1.0.1 分支  
可以重新编辑里面的代码  
```bash
git add README.md
git commit -m "修复 README.md 文件内容" 
git diff
git push origin hotfix/1.0.1
```
等待远程 github 仓库对这个 hotfix 分支的 Pull Requests 审核通过  
然后在 github -> Releases -> Create a new release ，选择对应的 tag 版本进行创建
```bash
git flow hotfix finish '1.0.1' #结束这个修复分支
git checkout main #再次回到 main 分支同步远程仓库的 tags
git fetch origin
git push --tags
```
一切结束后，回到 develop 分支继续其他功能的开发  
```bash
git checkout develop
git pull
```
















