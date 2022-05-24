# Makefile

## Summary

```
target ... : prerequisites ...
    command
    ...
    ...
```

target:

可以是一个object file(目标文件)，也可以是一个执行文件，还可以是一个标签(label)。对于标签这种特性，在后续的“伪目标”章节中会有叙述。

prerequisites:

生成该target所依赖的文件和/或target

command:

该target要执行的命令(任意的shell命令)

这是一个文件的依赖关系，也就是说，target这一个或多个的目标文件依赖于prerequisites中的文件，其生成规则定义在command中。说白一点就是说:
    prerequisites中如果有一个以上的文件比target文件要新的话, command所定义的命令就会被执行.

## `include`

## 变量

## 隐晦规则

## 工作方式

* 读入所有的Makefile。
* 读入被include的其它Makefile。
* 初始化文件中的变量。
* 推导隐晦规则，并分析所有规则。
* 为所有的目标文件创建依赖关系链。
* 根据依赖关系，决定哪些目标要重新生成。
* 执行生成命令。

## 很他妈坑的Makefile


# 参考资料

* [跟我一起写Makefile重置版](https://seisman.github.io/how-to-write-makefile/)
* [跟我一起写Makefile重置版(代码仓库)](https://github.com/seisman/how-to-write-makefile)
* [Makefile Tutorial By Example](https://makefiletutorial.com/)
* [Makefile Tutorial(代码仓库)](https://github.com/theicfire/makefiletutorial)

[INDEX](https://payne81.github.io/rookie_diary/)
