# Git 如何重命名远程分支

[资料][1]


> 在git中重命名远程分支，其实就是先删除远程分支，然后重命名本地分支，再重新提交一个远程分支。


需要把 dev_v_1.0.0 分支重命名为 dev_v_3.4.1 分支：

```shell
❯ git branch -av
 dev_v_1.0.0                                                c8eab409 sonar 扫描处理3

❯ git checkout dev_v_1.0.0
Switched to branch 'dev_v_1.0.0'
Your branch is up to date with 'origin/dev_v_1.0.0'.

❯ git push --delete origin dev_v_1.0.0
To https://git.xxxx.cn/x/xxx.git
 - [deleted]           dev_v_1.0.0


❯ git branch -m dev_v_1.0.0 dev_v_3.4.1

❯ git push origin dev_v_3.4.1
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: To create a merge request for dev_v_3.4.1, visit:
remote:   https://git.xxxx.cn/x/merge_requests/new?merge_request%5Bsource_branch%5D=dev_v_3.4.1
remote: 
To https://git.xxx.cn/x/xxx.git
 * [new branch]        dev_v_3.4.1 -> dev_v_3.4.1

```

以上远程分支已建立

关联本地分支和远程分支

```shell
❯ git status
On branch dev_v_3.4.1

❯ git branch --unset-upstream


❯ git branch --set-upstream-to=origin/dev_v_3.4.1 dev_v_3.4.1
Branch 'dev_v_3.4.1' set up to track remote branch 'dev_v_3.4.1' from 'origin'.

```




[1]: https://blog.zengrong.net/post/delete_git_remote_brahch/#%E9%87%8D%E5%91%BD%E5%90%8D%E8%BF%9C%E7%A8%8B%E5%88%86%E6%94%AF