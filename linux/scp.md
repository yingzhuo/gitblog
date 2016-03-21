# scp

#### 功能

命令格式: scp 选项 [用户名@地址:]文件名 [用户名@地址:]目录或文件

#### 常用

* `-r` 递归拷贝，拷贝目录时使用
* `-v` 显示连接等信息

```bash
scp ./logs.zip yingzhuo@10.211.55.13:/tmp
```

在脚本中scp往往配合`excpet`命令使用，如下，但需要注意的是，密码会以明文的方式暴露，慎用。

```
PASSWORD=123456

expect -c "
	spawn scp -r avatar.jpeg root@127.0.0.1:/tmp/
	expect \"password\"
	send \"$PASSWORD\r\"
	expect eof
"
```
