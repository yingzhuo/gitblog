# OpenLDAP

#### 1. 安装

```bash
sudo apt-get install slapd ldap-utils
```

#### 2. 配置

在`/etc/ldap`目录中应该有如下的文件。

```
-rw-r--r-- 1 root     root      332 2014-03-18 07:30:56 ldap.conf
drwxr-xr-x 2 root     root     4096 2015-09-16 03:19:58 sasl2/
drwxr-xr-x 2 root     root     4096 2016-04-04 07:19:19 schema/
drwxr-xr-x 3 openldap openldap 4096 2016-04-04 07:19:19 slapd.d/
```

但缺少了守护进程的配置文件`slapd.conf`，可以从配置文件模板中拷贝过来。<br>
模板文件为：`/usr/share/slapd/slapd.conf`

如果找不到，可以自行搜索一下。

```bash
find / -iname 'slapd.conf' -type f
```

之后拷贝过来，并备份。

```bash
cp /usr/share/slapd/slapd.conf /etc/ldap/slapd.conf
cp /etc/ldap/slapd.conf /etc/ldap/slapd.conf.ori
```

编辑该配置文件如下:

```
# This is the main slapd configuration file. See slapd.conf(5) for more
# info on the configuration options.

#######################################################################
# Global Directives:

# Features to permit
#allow bind_v2

# Schema and objectClass definitions
include         /etc/ldap/schema/core.schema
include         /etc/ldap/schema/cosine.schema
include         /etc/ldap/schema/nis.schema
include         /etc/ldap/schema/inetorgperson.schema

# Where the pid file is put. The init.d script
# will not stop the server if you change this.
pidfile         /var/run/slapd/slapd.pid

# List of arguments that were passed to the server
argsfile        /var/run/slapd/slapd.args

# Read slapd.conf(5) for possible values
loglevel        296

# Where the dynamically loaded modules are stored
modulepath	/usr/lib/ldap
moduleload	back_bdb.la

# The maximum number of entries that is returned for a search operation
sizelimit 500

# The tool-threads parameter sets the actual amount of cpu's that is used
# for indexing.
tool-threads 1

#######################################################################
# Specific Directives for database #1, of type @BACKEND@:
# Database specific directives apply to this databasse until another
# 'database' directive occurs
database        bdb

# The base of your directory in database #1
suffix          "dc=etiantian,dc=org"

# rootdn directive for specifying a superuser on the database. This is needed
# for syncrepl.
rootdn          "cn=admin,dc=etiantian,dc=org"
rootpw {SSHA}gx5g5QMSYjDIOJUfgsxw2P3HHGV5ApPU

# Where the database file are physically stored for database #1
directory       "/var/lib/ldap"

# The dbconfig settings are used to generate a DB_CONFIG file the first
# time slapd starts.  They do NOT override existing an existing DB_CONFIG
# file.  You should therefore change these settings in DB_CONFIG directly
# or remove DB_CONFIG and restart slapd for changes to take effect.

# For the Debian package we use 2MB as default but be sure to update this
# value if you have plenty of RAM
dbconfig set_cachesize 0 2097152 0

# Sven Hartge reported that he had to set this value incredibly high
# to get slapd running at all. See http://bugs.debian.org/303057 for more
# information.

# Number of objects that can be locked at the same time.
dbconfig set_lk_max_objects 1500
# Number of locks (both requested and granted)
dbconfig set_lk_max_locks 1500
# Number of lockers
dbconfig set_lk_max_lockers 1500

# Indexing options for database #1
index           objectClass eq

# Save the time that the entry gets modified, for database #1
lastmod         on

# Checkpoint the BerkeleyDB database periodically in case of system
# failure and to speed slapd shutdown.
checkpoint      2048 10

# Access Control
access to *
        by self write
        by anonymous auth
        by * read
```

其中，密码加密由工具生成

```
slappasswd -s 你的密码
```

删除`/etc/ldap/slapd.d/`下所有文件，当然，必须提前做好备份。

```bash
rm -rf /etc/ldap/slapd.d/*
```

生成OpenLDAP2.4格式的配置文件

```bash
slaptest -f /etc/ldap/slapd.conf -F /etc/ldap/slapd.d
```

注意，新生成的文件必须设置好user和group

```bash
chown -R openldap:openldap /etc/ldap/slapd.d
```

最后，重启OpenLDAP

```bash
/etc/init.d/slapd restart
```

最后的最后，可以验证一下。

```bash
ldapsearch -LLL -W -x ldap://etiantian.org -D "cn=admin,dc=etiantian,dc=org" -b "dc=etiantian,dc=org" "(uid=*)"
```

#### 3. 安装web管理工具

```
sudo apt-get update
sudo apt-get ldap-account-manager
```

安装`ldap-account-manager`依赖`httpd`，安装完成以后会启动其服务。

访问`http://yourhostname:80/lam/templates/login.php` <br>
"LAM configuration"默认管理密码为'lam'，应该尽快修改。
