# sed 和 awk
交互式与非交互式

文件操作与行操作

sed 一般用于对文本内容做替换

awk 一般用于对文本内容进行统计、按照需要的格式进行输出

## sed
替换命令
```shell
sed 's/old/new/' filename
sed -e 's/old/new/' -e 's/old/new/' filename ...
sed -i 's/old/new/' 's/old/new/' filename ...
```

## awk
- FS和OFS字段分隔符，OFS表示输出的字段分隔符
- RS记录分隔符
- NR和FNR行数
- NF字段数量，最后一个字段内容可以用$NF取出