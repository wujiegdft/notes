# dd - convert and copy a file

## example

### 磁盘写速度
```sh
time dd if=/dev/zero of=test.dat bs=1M count=128 conv=fdatasync
```

### 磁盘读速度
```sh
flush
echo 3 | sudo tee /proc/sys/vm/drop_caches
time dd if=test.dat bs=1M of=/dev/null count=3128
```


## params
- if=文件名：输入文件名，缺省为标准输入。即指定源文件
- of=文件名：输出文件名，缺省为标准输出。即指定目的文件
- ibs=bytes：一次读入bytes个字节，即指定一个块大小为bytes个字节
  
  obs=bytes：一次输出bytes个字节，即指定一个块大小为bytes个字节
  
  bs=bytes：同时设置读入/输出的块大小为bytes个字节
  
- cbs=bytes：一次转换bytes个字节，即指定转换缓冲区大小
- skip=blocks：从输入文件开头跳过blocks个块后再开始复制
- seek=blocks：从输出文件开头跳过blocks个块后再开始复制
- count=blocks：仅拷贝blocks个块，块大小等于ibs指定的字节数
- conv=<关键字>，关键字可以有以下11种：

  1、conversion：用指定的参数转换文件。
  
  2、ascii：转换ebcdic为ascii
  
  3、ebcdic：转换ascii为ebcdic
  
  4、ibm：转换ascii为alternate ebcdic
  
  5、block：把每一行转换为长度为cbs，不足部分用空格填充
  
  6、unblock：使每一行的长度都为cbs，不足部分用空格填充
  
  7、lcase：把大写字符转换为小写字符
  
  8、ucase：把小写字符转换为大写字符
  
  9、swab：交换输入的每对字节
  
  10、noerror：出错时不停止
  
  11、notrunc：不截短输出文件
  
  12、sync：将每个输入块填充到ibs个字节，不足部分用空（NUL）字符补齐。
  
