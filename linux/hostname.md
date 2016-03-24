# hostname

(本文档只针对Ubuntu)

* 功能: 显示或临时修改主机名
* 用法:

    ```bash
    # 显示主机名
    hostname

    # 临时修改主机名为 vm00
    hostname vm00
    ```

如果需要永久性变更主机名需要编辑一下两个文件

* `/etc/hostname`: 此文件保存着主机名
* `/etc/hosts`: 为ip指定名字
