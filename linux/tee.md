# tee

* 功能: 读取标准输入的数据，并将其内容输出成文件。
* 语法: tee [-ai][文件]
* 参数:
	* `-a` 或 `--append` 添加到文件，而不是覆盖
	* `-i` 或 `--ignore-interrupts` 忽略中断信号
* 例子:

	```
	who | tee who.out
	```
