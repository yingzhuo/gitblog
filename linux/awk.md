# awk

### 使用外部脚本

**任何严肃的开发工作都因采用外部脚本**

```bash
awk -f myscript.awk myfile.in
```

```awk
BEGIN {
    FS = ":"
}

{
    print $0
}
```

### 选择行

**在某种程度上可以取代grep指令的功能**

```awk
BEGIN {
    FS = ":"
}

! /^$/ { #只处理非空的行
    print $0
}
```

以上脚本等同于

```awk
BEGIN {
    FS = ":"
}

{
    if ($0 !~ /^$/) {
        print $0
    }
}
```

再看一个例子

```awk
BEGIN {
    FS = ":"
}

$2 == "root" {
    print $0
}
```

### 使用数字

```awk
BEGIN { x == 0 }
! /^$/ {
    x ++
}
END {
    printf "非空行共有%d行\n", x
}
```

其实字符串有时也可以当做数字来处理

```awk
BEGIN {
    x = "3.1415926"
}
{
    x = x + 1
}
```

### 常用的运算符

* `+` `-` `*` `/` `%`: 算术运算，与C语言中的运算符意义一致
* `&&` `||` `!`: 逻辑运算，与C语言中的运算符意义一致
* `++` `--`: 自增自减运算，与C语言中的云算法意义一致，awk语言也包含post，pre两种自增运算和自减运算。
* `==` `!=`: 相等/不等
* `~` `!~`: 正则匹配/正则不配

### 流程控制

**与C语言相似**

```awk
BEGIN {
    num = 10
}

{
    if ($1 == "foo") {
        print $1, $2, $3
    } else {
        print $1, $2, $4
    }

    for (i = 0; i < 100; i++) {
        print $1, $2, $3
    }

    while (1) {
        print $1, $2, $3
        if ($2 == "root") {
            break
        }
    }

    do {
        print $7, $8

        if ( num == 4 ) {
            continue
        }

        num --
    } while (num != 0)
}
```

### 常用隐含变量

```awk
BEGIN {
    FS = "[[:space:]+]"  # Filed Separators (正则) (输入)
    RS = "\n"            # Record Separators (字符串) (输入)

    OFS = ""             # Output Filed Separators (字符串) (输出)
    ORS = "\n"           # Output Record Separators (字符串) (输出)
}

{
    print NF            # Number of Field  (数字)
    print NR            # Number of Record (数字)
}
```
