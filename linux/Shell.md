# Shell

#### du -sh * 
查看文件大小

# 申明
\#!/bin/bash

# 变量赋值
c=$(ls -l /etc)

c=`ls -l /root`

ehco ${变量名}

# 变量删除
unset 变量名

# 特殊变量
$？ 判断上一个命令是否成功

$$ 当前进程号

$0 当前进程名称