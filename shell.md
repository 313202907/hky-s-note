# Shell
## Shell基础知识
 - `history`为输入命令历史
 - ``!!``执行上一条执行的指令
 - `!n`执行命令历史中的第n条指令
 - `!字符串`可以执行以改字符串为开头的最近的一条指令
 - **Tab**补全一个指令/路径/文件名，连按两次会列出所有符合的指令和文件名
 - Shell文件开头必须添加：`#!/bin/bash`
 - 编写Shell脚本后，需要将脚本设置为可执行权限：`chmod +x 114.sh`
 - 反引号　\`　中的内容会被**优先执行**，同`$()`

## Shell变量
### 定义变量
 ```
 your_name="yjspn.810"
 ```
 - 变量名和等号之间**不能有空格**
 - 只能使用英文字母，数字和下划线,**开头**不能为**数字**
 - 符号只能用**下划线**
 - 不能使用bash里的关键字

### 使用变量
```
your_name="yjspn"
echo $your_name
echo ${your_name}
```
 - 建议给变量加花括号
 - 使用变量时才使用`$`

### 变量操作
 - `readonly` 将变量变为只读
 - `unset` 删除变量，**只读的不能删除**

## Shell字符串

> 类似于php

### 单引号
 - 所有字符均**原样输出**，变量无效
 - 串内不能出现**单独**的单引号，*转义了也不行*，但是**能成对**出现

### 双引号
 - 可以有变量
 - 可以有转义字符

### 获取字符串长度方法之一
```
echo ${#str}
```

## Shell数组

### 定义数组

```
array_name=(value0 value1 value2 value3)
```
 - 用空格分开，批量定义
 - 竖过来也行，还是要加空格
 - 单独定义：`array_name[0]=value0`

 ### 读取数组
 ```
 echo ${array_name[@]}
 ```

 ### 获取数组长度方法之一
 ```
 # 取得数组元素的个数
length=${#array_name[@]}
# 或者
length=${#array_name[*]}
# 取得数组单个元素的长度
lengthn=${#array_name[n]}
 ```

## Shell注释

### 通用
行首加`#`

### 多行注释
```
<<'EOF'
注释内容...
注释内容...
注释内容...
EOF
```
 - EOF可以替换为其他字符串或者符号
 - 仅推荐这种注释方法

## Shell传递参数
 - 脚本内获取参数的格式为：`$n`
 - **$0**为**文件名**
 - n 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推

| 参数处理 | 说明 |
| ---- | ---- |
|$# | 传递到脚本的参数**个数**|
$* | 以一个单字符串显示所有向脚本传递的参数。如"$*"用「"」括起来的情况、**以"$1 $2 … $n"的形式**输出所有参数。|
$$ | 脚本运行的当前进程ID号|
$! | 后台运行的最后一个进程的ID号|
$@ | 与$\*相同，但是使用时加引号，并在引号中返回每个参数。如"$@"用「"」括起来的情况、**以"$1" "$2" … "$n" 的形式**输出所有参数。|
$- | 显示Shell使用的当前选项，与set命令功能相同。
$? | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。|

#### $* 与 $@ 区别
 - 相同点：都是引用所有参数。
  - 不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则 " * " 等价于 "1 2 3"（传递了**一个**参数），而 "@" 等价于 "1" "2" "3"（传递了**三个**参数）。

## Shell基本运算符

### 算数运算符

 - 乘号`*`前必须加反斜杠`\`才能实现乘法运算.

 - 条件表达式要放在**方括号之间**，并且要有**空格**，例如: [$a==$b] 是错误的，必须写成 **[ $a == $b ]**。

### 关系运算符

 > 只支持数字，不支持字符串，除非字符串的值是数字

 | 运算符 | 说明 | 举例 |
 | ---- | ---- | ---- |
 |-eq | 检测两个数是否相等，相等返回 true。| `[ $a -eq $b ]` 返回 `false`。 |
 |-ne | 检测两个数是否不相等，不相等返回 true。| `[ $a -ne $b ]` 返回 `true`。 |
 |-gt | 检测左边的数是否大于右边的，如果是，则返回 true。| `[ $a -gt $b ]` 返回 `false`。 |
 |-lt | 检测左边的数是否小于右边的，如果是，则返回 true。| `[ $a -lt $b ]` 返回 `true`。 |
 |-ge | 检测左边的数是否大于等于右边的，如果是，则返回 true。| `[ $a -ge $b ]` 返回 `false`。 |
 |-le | 检测左边的数是否小于等于右边的，如果是，则返回 true。| `[ $a -le $b ]` 返回 `true`。 |

### 布尔运算符

|运算符|说明|举例|
|----|----|----|
|!|非运算，表达式为 true 则返回 false，否则返回 true。|`[ ! false ]` 返回 `true`。|
-o|或运算，有一个表达式为 true 则返回 true。|`[ $a -lt 20 -o $b -gt 100 ]` 返回 `true`。|
-a|与运算，两个表达式都为 true 才返回 true。|`[ $a -lt 20 -a $b -gt 100 ]` 返回 `false`。|

