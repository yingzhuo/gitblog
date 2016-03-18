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

#### 3. 钩子

常用`pre-commit`钩子

如：

```bash
#!/usr/bin/env bash
#
# PRE-COMMIT HOOK
#
# The pre-commit hook is invoked before a Subversion txn is
# committed.  Subversion runs this hook by invoking a program
# (script, executable, binary, etc.) named 'pre-commit' (for which
# this file is a template), with the following ordered arguments:
#
#   [1] REPOS-PATH   (the path to this repository)
#   [2] TXN-NAME     (the name of the txn about to be committed)
#
#   [STDIN] LOCK-TOKENS ** the lock tokens are passed via STDIN.
#
#   If STDIN contains the line "LOCK-TOKENS:\n" (the "\n" denotes a
#   single newline), the lines following it are the lock tokens for
#   this commit.  The end of the list is marked by a line containing
#   only a newline character.
#
#   Each lock token line consists of a URI-escaped path, followed
#   by the separator character '|', followed by the lock token string,
#   followed by a newline.
#
# The default working directory for the invocation is undefined, so
# the program should set one explicitly if it cares.
#
# If the hook program exits with success, the txn is committed; but
# if it exits with failure (non-zero), the txn is aborted, no commit
# takes place, and STDERR is returned to the client.   The hook
# program can use the 'svnlook' utility to help it examine the txn.
#
# On a Unix system, the normal procedure is to have 'pre-commit'
# invoke other programs to do the real work, though it may do the
# work itself too.
#
#   ***  NOTE: THE HOOK PROGRAM MUST NOT MODIFY THE TXN, EXCEPT  ***
#   ***  FOR REVISION PROPERTIES (like svn:log or svn:author).   ***
#
#   This is why we recommend using the read-only 'svnlook' utility.
#   In the future, Subversion may enforce the rule that pre-commit
#   hooks should not modify the versioned data in txns, or else come
#   up with a mechanism to make it safe to do so (by informing the
#   committing client of the changes).  However, right now neither
#   mechanism is implemented, so hook writers just have to be careful.
#
# Note that 'pre-commit' must be executable by the user(s) who will
# invoke it (typically the user httpd runs as), and that user must
# have filesystem-level permission to access the repository.
#
# On a Windows system, you should name the hook program
# 'pre-commit.bat' or 'pre-commit.exe',
# but the basic idea is the same.
#
# The hook program typically does not inherit the environment of
# its parent process.  For example, a common problem is for the
# PATH environment variable to not be set to its usual value, so
# that subprograms fail to launch unless invoked via absolute path.
# If you're having unexpected problems with a hook program, the
# culprit may be unusual (or missing) environment variables.
#
# Here is an example hook script, for a Unix /bin/sh interpreter.
# For more examples and pre-written hooks, see those in
# /usr/share/subversion/hook-scripts, and in the repository at
# http://svn.apache.org/repos/asf/subversion/trunk/tools/hook-scripts/ and
# http://svn.apache.org/repos/asf/subversion/trunk/contrib/hook-scripts/

REPOS="$1"
TXN="$2"

MAX_SIZE=10240000
MIN_LOG=10
FILTER='\.(zip|rar|jar|bz2|gz|tar|war|ear)$'
SVNLOOK=/usr/bin/svnlook

# Make sure that the log message contains some text.
LOGMSG=$($SVNLOOK log -t "$TXN" "$REPOS" | grep "[a-zA-Z0-9]" | wc -c)
if [ "$LOGMSG" -lt $MIN_LOG ]
then
    echo -e "Please enter at least $MIN_LOG characters for log message." >&2
    exit 1
fi

files=$($SVNLOOK changed -t $TXN $REPOS | awk '{print $2}')
for f in $files
do
    #check file type
    if echo $f |tr A-Z a-z | grep -Eq $FILTER
    then
        echo "File $f is not allow to commit." >&2
        exit 1
    fi

    #check file size
    filesize=$($SVNLOOK cat -t $TXN $REPOS $f | wc -c)
    if [ "$filesize" -gt "$MAX_SIZE"]
    then
        echo "File $f is too large." >&2
        exit 1
    fi
done

#All checks passed, so allow the commit.
exit 0
```
