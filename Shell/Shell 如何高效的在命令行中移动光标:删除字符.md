### Shell 如何高效的在命令行中移动光标/删除字符

#### Mac 环境

熟练度分 新手 / 老手 / 专家
> 新手在最上面（有机会看到的话就看看；专家在最下面（已经掌握的习惯仅作为记录

##### 命令行 光标移动 && 删除字符

- control + a 跳到本行的行首 
> 熟练度：新手
> a=ahead ?
- control + e 跳到本行的行尾 
> 熟练度：新手
> e=end ?
- control + w / d 删除单词，w=删除光标前面的单词 d=删除光标后面的单词 
> 熟练度：新手
> w=word d=delete ?
- control + k / u 删除光标前后内容，k=删除光标后面的文字 u=删除光标前面的文字 
> 熟练度：新手
> k=killall u= ?
- control + b / f 移动光标（按字符，b=向后移动 f=向前移动
> 熟练度：新手
> b=before f=forward
- control + y 粘贴或回复上次的删除（只有上一次，不是 control + z）（原理是 所有的删除都是剪切，很棒的理解，来自庄嘉祥）
> 熟练度：新手
> y=yes ???
- control + l 清屏 = clear
> 熟练度：新手
> l=clear(l)
- control + t 交换两个字符
> 熟练度：新手
> t=translate
- control + x 交换当前光标和行首光标的位置
> 熟练度：新手
> x=exchange(x)
- esc + f / b 移动光标（按词，b=向后移动 f=向前移动
> 熟练度：新手
> b=before f=forward
> 不大实用，每次只能移动一次单词。。。


---

- control + c 退出当前编辑行
> 熟练度：专家
> c=cancel
- control + r 搜索之前运行命令
> 熟练度：老手
> c=cancel


---

#### 为何很多 linux 系统的操作命令是通用的？ 比如 vi 和 命令行

从其中一篇[熟悉 Bash 快捷键来提高效率][1]中提到，
> Bash快捷键其实是GNU Readline快捷键， GNU Readline Library是一个来接受用户输入的GNU软件包。

说明其实很多都用了底层的 GNU Readline Lib，包括OSX/Linux 所以特别好。

[1]: https://harttle.land/2015/11/09/bash-shortcuts.html
