# wget

* 功能: 下载文件
* 例子:

  ```
  # 下载到指定目录
  wget "http://www.163.com" -P /tmp

  # 下载并重命名
  wget "http://www.163.com" -O /tmp/163.index.html

  # 通过https协议下载
  wget "http://www.163.com" -O /tmp/163.index.html --no-check-certificate
  ```
