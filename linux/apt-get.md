# apt-get

常用命令

```bash
# 搜索软件包
apt-cache search {package}

# 获取包的相关信息，如说明、大小、版本等
apt-cache show {package}

# 安装软件包(常用)
sudo apt-get install {package}

# 重新安装软件包
sudo apt-get install {package} --reinstall

# 修复安装软件包
sudo apt-get -f install

# 删除软件包
sudo apt-get remove {package}

# 删除软件包，含配置文件等
sudo apt-get remove {package} --purge

# 更新源
sudo apt-get update  

# 更新已安装的包
sudo apt-get upgrade

# 升级系统
sudo apt-get dist-upgrade

# 了解使用该包依赖那些包
apt-cache depends {package}

# 查看该包被哪些包依赖
apt-cache rdepends {package}

# 安装相关的编译环境
sudo apt-get build-dep {package}

# 下载该包的源代码
apt-get source {package}

# 清理无用的包
sudo apt-get clean && sudo apt-get autoclean

# 检查是否有损坏的依赖
sudo apt-get check
```