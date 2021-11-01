#### 一个流程
    git init // 初始化一个仓库
    git add -A // 添加所有文件到暂存区，也就是交给由git管理着
    git commit -m "myblogs first commit" // 提交到git仓库，-m后面是注释
    git remote add origin https://github.com/xxx/myblogs.git
    git push -u origin master // 推送到远程myblogs仓库

#### gitHub Demo
    // Git global setup
    git config --global user.name "xiaosi"
    git config --global user.email "annie.zhao@qq.com"

    // Create a new repository
    git clone https://git.xxx.git
    cd frontent-vue
    git switch -c main
    touch README.md
    git add README.md
    git commit -m "add README"

    // Push an existing folder
    cd existing_folder
    git init --initial-branch=main
    git remote add origin https://git.xxx.git
    git add .
    git commit -m "Initial commit"

    // Push an existing Git repository
    cd existing_repo
    git remote rename origin old-origin
    git remote add origin https://git.xxx.git

#### git代理服务器

!> 443错误码 ---> 解决方案： 检查代理

* 设置http、https代理
```
git config --global http.proxy 'http://127.0.0.1:1080'
git config --global https.proxy 'http://127.0.0.1:1080'
```
* 查看http、https代理
```
git config --global --get http.proxy
git config --global --get https.proxy
```
* 取消http、https代理
```
git config --global --unset http.proxy
git config --global --unset https.proxy
```

!>  git的两种clone： http和ssh

#### git add -A 和 git add . 的区别

https://www.cnblogs.com/skura23/p/5859243.html