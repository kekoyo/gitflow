# gitflow
测试 gitflow 流程  

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
并且会自动切换到 `develop` 分支，然后创建一个 `feature` 功能分支  

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
git pull
```


