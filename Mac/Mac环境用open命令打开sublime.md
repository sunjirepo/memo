Mac环境用open命令打开sublime


1 基础命令 open -a Sublime\ Text {文件名}
man open;
...
	-a application
         Specifies the application to use for opening the file
...

2 修改 sublime 应用程序名称

直接在 Finder / Applications 文件里修改 'Sublime Text.app' => 'sublime.app'

3 验证, 命令行
$ sublime --help


4 优化版本

open -a sublime {文件名}