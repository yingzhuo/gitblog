# Shell Cookbook

#### 判断当前用户是否为`root`用户

```bash
if [[ $EUID -ne 0 ]]; then
    echo "[NG] This script must be run as root." 1>&2
    exit 1
else
    # do something here.
    exit 0
fi
```