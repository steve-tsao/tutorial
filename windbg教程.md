### 支持三类命令

内部命令：操作被调试目标

元命令：以(.)开头，操作调试器本身

扩展命令：以(!)开头，调试器默认加载一些预定义扩展命令，还可编写扩展DLL增加命令

### 常用命令

##### 用户模式

`.symfix`快速设置符号信息

`~`显示被调用进程内部的所有线程信息

- 线程列表前的(.)为当前要操作的线程

- 线程列表前的(#)为当前断点暂停所在的线程

`~ns`切换当前线程，n为线程索引

`lm`显示当前线程的模块信息，模块有4种状态如下：

- deferred: 符号还未装入

- pdb symbol：公开符号已被装入

- export symbol：该DLL只有导出符号，本模块没有符号或还没找到

- no symbol：导出符号和本模块符号都没有，一般是可执行文件或驱动文件

`.reload /f modulename.dll`强制加载模块符号

`k`栈回溯

`~nk`线程n的栈回溯

`？`进制转换，windbg中默认为16进制

- ？后跟16进制数，可查看与之对应的10进制

- ？后跟0n十进制数，可查看与之对应的16进制

`!teb`查看线程teb

- stackbase和stacklimit: 当前线程用户模式栈基址和限制

- clientid: 进程和线程id

- lasterrorvalue: 上一个win32错误代码

- tlsstorage: 线程的线程局部存储数组

`dt modulename!structname`查看结构体详情

`.prefer_dml 1`打开调试器跳转结构体的超链接

`bp modulname!functionname`在该方法处下断点

`bl`查看断点列表

`r registername`查看寄存器值

`db address`字节方式显示内存，右边为ascii字符

`db @registername`直接查看寄存器指向的内存

`du`显示unicode字符

`u`反汇编列出接下来8条指令

`p`步过

`t`步入

`!error @eax`查看函数返回值(x64函数返回值保存在eax或rax)

`bd *`禁止所有断点

`bu`为尚未加载的例程名称设置断点，该断点称为延迟、 虚拟或未解析的断点。

##### 内核模式

###### 本地内核模式

本地内核调试需要开启系统调试模式，命令行`bcdedit /debug on`

`!process 0 0`显示系统中所有进程信息，第一个0表示所有进程，第二个0表示信息详细程度

`!process 0 0 processname`指定进程

`!process processaddress 1`指定进程地址和更多细节

###### 完整内核模式

vmware添加串口

- 使用命名管道\\\\.\pipe\pipename
- 该端是服务器，另一端是应用程序

windbg开启内核调试选择串口模式

- 勾选pipe，reconnect

- 设置port为\\\\.\pipe\pipename

被调试机设置端口重启

- bcdedit /debug on

- bcdedit /dbgsettings serial debugport:2 baudrate:115200(debugport应该是vmware添加的串口号)

- 重启

凌讯网络


