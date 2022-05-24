# awk&sed&grep

* awk: 流式编辑器
* sed: 非交互流式文本编辑器,可以对文本文件进行增,删,改,查等操作
* grep: 模式匹配

# awk
#### 概览

awk(默认以换行符分隔)逐行读入文件,默认空格分隔一行中的每一列,针对特定部分进行处理. 参考[CSDN awk命令详解](https://blog.csdn.net/anqixiang/article/details/117903529),其余命令也可参考C语言中文网的[linux教程](http://c.biancheng.net/linux_tutorial/text_processing/)
```
Usage:      awk [-F|-f|-v] 'BEGIN{} //{command1; command2} END{}' file
[-F|-f|-v]  参数,-F指定(列)分隔符,-f调用脚本,-v定义变量(自定变量或者awk已有变量) var=value
'  '        引用代码块
BEGIN       初始化代码块,在对每一行进行处理之前执行
//          匹配代码块,可以是字符串或正则表达式
{}          命令代码块,包含一条或多条命令
;           多条命令使用分号分隔
END         结尾代码块,在对每一行进行处理之后执行
```

#### 参数
```
$0          表示整个当前行
$1          每行第一个字段, 以此类推..
NF          字段数量变量
NR          每行的记录号,多文件记录递增
FNR         与NR类似,不过多文件记录不递增,每个文件都从1开始
FILENAME    当前文件名
```

#### 指定分隔符
```
-F:         指定输入中':'是列分隔符
-F'[:./]'   ':', '.', '/'都可以作为分隔符
FS          输入字段分隔符
RS          输入的行分隔符,默认为换行符(即文本是按一行一行输入). eg. -v RS="." 
OFS         输出字段分隔符,默认也是空格,可以改为制表符等. eg. -v OFS="\t"
ORS         输出的行分隔符,默认为换行符,即处理结果也是一行一行输出到屏幕. eg. -v ORS="?"
```

#### 匹配
```
awk '/localhost/' /tmp/hosts
awk '$3~/local/' /tmp/hosts             #每行的第3列去匹配local
awk '$3~/local/{print $1,$2}' /tmp/hosts
awk '$2=="localhost"' /tmp/hosts        #第2列精确匹配localhost
awk '$2!="localhost"' /tmp/hosts        #取反
awk -F: '$3<=10' /etc/passwd            #第3列小于等于10的行
awk -F: 'NR==10' /etc/passwd            #仅显示第10行
awk -F: '$3>1 && $3<5' /etc/passwd      #逻辑与
awk -F: '$3==1 || $3==5' /etc/passwd    #逻辑或

e.g.
awk '/bash$/{x++} END{print x}' /etc/passwd         # 匹配到以bash结尾的行时, x++, 最后输出x
```

# sed
#### 概览

sed每次读取文件一行内容,根据提供的规则命令匹配并修改数据,(默认不会直接修改源文件数据.而是会将数据复制到缓冲区中.修改也仅限于缓冲区中的数据), 然后输出执行结果.

```
Usage:      sed [选项] [脚本命令] 文件名
-e  file    将其后跟的脚本命令添加到已有的命令中。
-f  file    将其后文件中的脚本命令添加到已有的命令中。
-n          默认情况下.sed 会在所有的脚本指定执行完毕后.会自动输出处理后的内容.而该选项会屏蔽启动输出.需使用 print 命令来完成输出。
-i          直接修改源文件
```


# 引用
* [CSDN awk命令详解](https://blog.csdn.net/anqixiang/article/details/117903529)
* [C语言中文网 linux教程](http://c.biancheng.net/linux_tutorial/text_processing/)

[INDEX](https://payne81.github.io/rookie_diary/)
