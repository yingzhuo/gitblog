# SVN

#### 1. 安装

安装无比轻松，只需要一条命令即可。

```
sudo apt-get install subversion
```

#### 2. 配置

为了方便统一管理，SVN数据和账户信息统一保存在`/application`目录。

新建如下两个目录。

* `/application/svndata`
* `/application/svnpasswd`

在`/application/svnpasswd`下创建两个文件

```
touch /application/svnpasswd/passwd
touch /application/svnpasswd/authz
```

分别编辑内容如下:

`passwd`文件用来记录用户信息 <br>
如下文件所示，添加了两个用户，一个名为`yingzhuo`，另一个名为`wenjingjing`。

```
### This file is an example password file for svnserve.
### Its format is similar to that of svnserve.conf. As shown in the
### example below it contains one section labelled [users].
### The name and password for each user follow, one account per line.

[users]
# harry = harryssecret
# sally = sallyssecret
yingzhuo = yingzhuo
wenjingjing = wenjingjing
```

`authz`文件用来管理用户和组的信息 <br>
如下文件所示，指定了上述的两个用户在`sadoc`项目的权限。

```
### This file is an example authorization file for svnserve.
### Its format is identical to that of mod_authz_svn authorization
### files.
### As shown below each section defines authorizations for the path and
### (optional) repository specified by the section name.
### The authorizations follow. An authorization line can refer to:
###  - a single user,
###  - a group of users defined in a special [groups] section,
###  - an alias defined in a special [aliases] section,
###  - all authenticated users, using the '$authenticated' token,
###  - only anonymous users, using the '$anonymous' token,
###  - anyone, using the '*' wildcard.
###
### A match can be inverted by prefixing the rule with '~'. Rules can
### grant read ('r') access, read-write ('rw') access, or no access
### ('').

[aliases]
# joe = /C=XZ/ST=Dessert/L=Snake City/O=Snake Oil, Ltd./OU=Research Institute/CN=Joe Average

[groups]
# harry_and_sally = harry,sally
# harry_sally_and_joe = harry,sally,&joe
yingzhuo = yingzhuo,wenjingjing

# [/foo/bar]
# harry = rw
# &joe = r
# * =

# [repository:/baz/fuz]
# @harry_and_sally = rw
# * = r

[sadoc:/]
yingzhuo = rw
wenjingjing = r
```

启动服务器

```
svnserve -d -r /application/svndata/ --pid-file=/application/svndata/svn.pid
```

新建repository

```
svnadmin create sadoc
```

编辑`/application/svndata/sadoc/conf/svnserve.cnf`

```
anon-access = none # 不允许匿名访问
auth-access = write # 允许授权访问
password-db = /application/svnpasswd/passwd # 指定用户文件位置
authz-db = /application/svnpasswd/authz # 指定授权文件位置
```

最后重启SVN服务即可。
