# Git 如何显示中文文件名称

环境：Mac

git status 遇到中文文件时返回 \xxx\xxx 格式
```shell
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   "\346\257\217\345\221\250\350\256\260\345\275\225\357\274\2102020\357\274\211"

no changes added to commit (use "git add" and/or "git commit -a")
```

**输入如下命令即可**

```shell
#不对0x80以上的字符进行quote，解决git status/commit时中文文件名乱码
git config --global core.quotepath false
```

