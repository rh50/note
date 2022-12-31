
# 关于awk中NR、FNR、NF、$NF、FS、OFS的说明

## NR和FNR
    NR: 表示当前读取的行数
    FNR: 当前修改了多少行

## NF和$NF
    NF: 浏览记录的域的个数
    $NF: 最后一个列，输出最后一个列的内容

## FS和OFS
    FS: 指定列分隔符，当FS为空的时候，awk会把一行中的每个字符，当成一列来处理。
    OFS: 列输出分隔符
