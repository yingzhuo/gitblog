# Github下载单个文件

[参考](http://stackoverflow.com/questions/4604663/download-single-files-from-github)

下载地址为:

```
https://raw.githubusercontent.com/{user}/{repository}/{branch}/path_to_filename
```
* user: Github用户名
* repository: 仓库名
* branch: 分支名

如此，可利用`wget`工具直接下载。

**Note:** 本技巧之适合下载文本文件。
