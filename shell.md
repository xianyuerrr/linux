# shell
Shell是命令解释器，用于解释用户对操作系统的操作。有很多种shell，在`cat/etc/shells`文件夹下。CentOS 7 默认使用的Shell是bash。

Linux的启动过程：`BIOS-MBR-BootLoader（grub）-kernel-systemd-系统初始化-shell`

`#`开头的是注释

`chmod u+rx filename`，为shell文件赋予执行权限

## 执行
四种执行方式：
- `bash shellscript.sh`，对当前环境无影响
- `./shellscript.sh`，对当前环境无影响
- `. shellscript.sh`
- `source shellscript.sh`


## 通配符
- `*`，匹配任意字符串
- `?`，匹配一个字符串
- `[xyz]`，匹配xyz任一字符
- `[a-z]`，匹配范围内的字符
- `[!xyz]`或`[^xyz]`，不匹配


## 管道与重定向
- 管道符：`|`，将前一个命令执行的结果传递给后面的命令。
- 输入重定向：`<`，e.g.：`read var < /path/to/a/file`
- 输出重定向：`>`（清空文件）、`>>`（追加文件）、`2>`（错误重定向）、`&>`（全重定向），e.g.：`echo 123 > /path/to/a/file`
- 组合使用：`cat > /path/to/a/file << EOF`


## 变量
命名规则：
- 字母、数字、下划线
- 不能以数字开头

赋值：
- `a=123`
- `let a=123`
- `l=ls`
- `l=$(ls -l /etc)`，除了$()也可以使用``
- `l=ls`

- 导出：`export`
- 删除：`unset`


## 系统环境变量
环境变量：
- `set`和`env`
- `$?`，上一条命令是否执行失败
- `$$`，显示当前进程PID
- `$0`：显示当前进程名称
- `$1`、`$2`等：位置参数
- `$*`和`$@`，代表所有位置参数
- `$#`，代表位置参数的数量
- `PATH`
- `$PS1`

配置文件（按照加载顺序）：
- /etc/profile
- /etc/profile.d/
- ~/.bash_profile
- ~/.bashrc
- /etc/bashrc

## 数组
定义数组：`IPTS=（10.0.0.110.0.0.210.0.0.3`

- 显示数组的所有元素：`echo ${IPTS[@l}`
- 显示数组元素个数`echo ${#IPTS[@l}`
- 显示数组的第一个元素`echo $IPTS[0]}`


## 转义与引用
特殊字符：
- `#`：注释
- `;`：分号
- `\`：转义符
- `"`和`'`：引号


## 括号
()，圆括号
- 单独使用圆括号会产生一个子shell`(xyz=123)`
- 数组初始化`IPS=(ip1 ip2 ip3)`

[]、[[]]，方括号
- 单独使用方括号是测试（test）或数组元素功能
- 两个方括号表示测试表达式

<>尖括号重定向符号

{}，花括号
- 输出范围`echo{0..9}`
- 文件复制`cp/etc/passwd{.bak}`

## 测试与判断
```shell
if [$USER = root]; then
    echo "user root"
elif [$USER = xianyue]; then
    echo "user xianyue"
else
    echo "user other"
fi
```

```shell
case "$变量" in
    "情况1" )
        命令;;
    "情况2" )
        命令;;
esac
```


## 循环
```shell
for i in {1..9}
do
    echo $i
done
```

```shell
for ((i=1; i < 10; i++))
do
    echo $i
done
```

```shell
a=1
while [ $a -lt 10 ]
do
    echo $a
    ((a++))
done
```


## 函数
```shell
function fname(){
    echo "function"
}
```


## 优先级
fork炸弹：`.(){.|.&};.`


## 信号
`trap "echo sig 15" 15`


## 计划任务
一次性，`at 18:31"`

周期性，`crontab -e`，`* * * * * date >> /tmp/date.txt`

加锁