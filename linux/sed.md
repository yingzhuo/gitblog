# sed

### 使用外部脚本

**任何严肃的开发工作都因采用外部脚本**

```bash
sed -f myscript.sed myfile.in
```

### 命令基本形式

sed -e '[选择][动作]' myfile.in

**选择说明:**

* 指定行号选择: `[n1,n2]function`
    * `1,3function`   - 选择1到3行
    * `100,$function` - 选择100到最末一行
* 通过正则选择: `/regex/function`
    * `/^$/function` - 选择空行
    * `/^\s*$/function` - 选择空白行
    * `/^#.*$/function` - 选择以`#`开始的行

**动作说明:**

* a - 添加一行在指定行的下方
    * `1a "xxxxx"` - 在第一行下方添加一行，内容为`xxxxx`
* i - 插入新行在指定行的上方
    * `10i "xxxxx"` - 在第10行上方添加加一行，内容为`xxxxx`
* c - 取代某一行
    * `1c "xxxxx"` - 第一行替换成 `xxxxx`
* d - 删除指定的行
    * `/^#.*$/d` - 删除注释行 (`#`开头的行)
    * `/^\s*$/d` - 删除空白行
* s - 替换
    * `s/line/LINE/g` - 将`line`替换成`LINE`

### 连续执行多个动作

例子:

```
sed -n -e '/^line.*$/{s/line/@LINE/g;p} myfile.in'
```
