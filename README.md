# linux_study
linux学习笔记


# shell基础
- echo
	- -e使用转义字符
- first bash
```bash
#!/bin/bash
#my first program
#Author:Mr.Robot
echo -e "Mr.Robot是世界上最帅的男人！"
```
- windows下编辑的shell脚本的换行符是 ^M$，而linux是$,如果想将windows下的shell转为linux下的shell,只需dos2unix即可，同样相反的转换只需unix2dos
- history 实时查看命令历史记录
  - -c clear history command
  - -w 把缓存中的历史命令写入历史命令保存文件——~/.bash_history
  - 默认保存1000条历史记录，但是可以在/etc/profile中修改
  ```bash
  HISTSIZE=XXX
  ```
  - 但是必须重新登录，修改才能生效
  - !n 重复执行第n条命令
  - !! 重复执行上一条命令
  - !字符串 重复执行最后一条以该字符串开头的命令
- alias 别名=“原命令“
  - 将alias语句写入/etc/bashrc中可以使得别名永久生效
- 命令执行顺序
  - 第一顺位执行用绝对/相对路径执行的命令
  - 第二顺位执行别名
  - 第三顺位执行bash的内部命令
  - 第四顺位执行按照$PATH环境变量定义的目录查找顺序找到的第一个命令
- BASH快捷键大全
	待补全
- 输出重定向：
	- 输出信息
		- ">" 覆盖方式
		- ">>" 追加方式
	- 报错信息
		- 2> 覆盖方式
		- 2>> 追加方式
	- 命令 &> /dev/null 无论该条命令正确与否、统统丢进垃圾箱
- 输入重定向：
	- 命令 < 文件
- 多命令顺序执行
	- 命令1 ; 命令2  多条命令依次执行，之间没有任何关系
	- order1 && order2 逻辑与、order1必须正确执行，order2才会执行
	- order1 || order2 逻辑或  只有在order1执行不正确时，order2才会执行
	- 应用： order && echo yes || echo no
- dd命令
	- dd命令能复制file、system、分区、甚至整个硬盘，增强版cp
	- 使用格式:
	```shell
dd if=INPUT_FILE of=OUT_FILE bs=字节数 count=个数
	```
- | 管道符
	- order1 | order2  order1的正确执行结果作为order2的操作对象
- grep [选项] "搜索内容" 文件名
	- 在文件中搜索包含有关键字的行
	- "-i"  忽略大小写
	- "-n"  输出行号
	- "-v"  反向查找
	- "--color=auto"  搜索出的关键字用颜色显示
	- 例如： netstat -ano | grep ESTABLISHED 查看当前计算机连接数
## Bash基本功能
- 通配符
	- ? 匹配一个字符
	- * 匹配当前目录下的所有
	- [abc]  同regx
	- [a-c]  同regx
	- "\[^a-c]" "\[^abc]"  同regx
- 环境变量
	- 声明
  ```shell
  export 变量名=变量值
  ```
	- 查看 env
	- PATH: 是系统查找命令的路径
	- 配置PATH  PATH="PATH":路径i   ：表示变量叠加
- PS1
	- 定义系统命令提示符的变量
- 参数变量
	- 将命令行调用脚本时给的参数传到脚本内部
	- $0、...、$9 大于10的变量需要${10}
	- $*所有参数
	- $@所有参数、但是对于每个参数区别对待
		- 例如$@得到的参数集合可以将参数看成一个参数列表进行遍历。
	- $#传进来的所有参数的个数
- 预定义变量
|预定义变量|作用|
|-|-|
|$?|最后一次执行的命令的返回状态。0为正确执行，非0为不正确执行.&& \|\| 命令的逻辑与或中的逻辑短路就是依照此变量的值而实现的|
|$$|当前进程的PID|
|$!|后台运行的最后一个进程的PID|
- 接受键盘输入
	- read [选项] [变量名]
	- 选项
		- -p  提示信息
		- -t  等待的秒数、若没有则一直等待
		- -n  字符数，接受指定的字符数
		- -s  不回显
### 变量测试








