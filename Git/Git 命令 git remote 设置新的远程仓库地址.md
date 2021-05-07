# Git 命令 git remote 设置新的远程仓库地址

某些情况下需要更换远程仓库地址

```shell
# 查看关联的远程仓库的详细信息
git remote -v

# origin  git@xxx/algorithm-admin-server.git (fetch)
# origin  git@xxx/algorithm-admin-server.git (push)

# 删除关联的远程仓库
git remote remove origin

git remote -v

# 添加新的远程仓库关联
git remote add origin <url>

git remote -v

# origin  <url>/algorithm-admin-server.git (fetch)
# origin  <url>/algorithm-admin-server.git (push)

```

git remote add origin git@github.com:sunjirepo/common-parent.git


git remote add origin git@git.corp.hrtps.com:java-common/common-cloud-server.git