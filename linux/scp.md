# scp

#### 功能

命令格式: scp 选项 [用户名@地址:]文件名 [用户名@地址:]目录或文件

#### 常用

* `-r` 递归拷贝，拷贝目录时使用
* `-v` 显示连接等信息

```bash
scp ./logs.zip yingzhuo@10.211.55.13:/tmp

PASSWORD=****

expect -c "
	spawn scp -r avatar.jpeg root@127.0.0.1:/tmp/
	expect \"password\"
	send \"$PASSWORD\r\"
	expect eof
"
```
