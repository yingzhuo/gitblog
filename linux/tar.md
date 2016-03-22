# tar

压缩或解压缩文件或目录

```bash
# 压缩文件
tar -zvcf dir.tar.gz dir/
tar -jvcf dir.tar.bz2 dir/
tar -vcf dir.tar dir/

# 查看压缩文件内容
tar -zvtf dir.tar.gz
tar -jvtf dir.tar.bz2
tar -vtf dir.tar

# 解压缩
tar -zvxf dir.tar.gz -C .
tar -jvxf dir.tar.bz2 -C .
tar -vxf dir.tar -C .
```
