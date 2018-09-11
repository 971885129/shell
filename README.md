# shell
## 权限设置
umask 022 设置新建文件或目录的权限，新文件权限为（666-022=644），新目录的权限为（777-022=755）
<br>修改文件权限 chmod 755 file 
<br>修改文件属主 chown  wxm test.txt  
<br>修改文件所属组 chgrp  group1 text.txt 
<br>修改用户所属组 usermod -G manage wxm 会保留原来所在的组
<br>查看用户所在组 groups wxm
## 变量赋值
a=aa
<br>b=bb
<br>echo $a 
## 字符串拼接
c=${a}_vs_${b}
<br>打印输出结果为a_vs_b
## 调用R脚本
cat test.R | R --vanilla --slave --args <参数1>
<br>传入的第一个参数为args[5]
<br>Rscript test.R <参数1>
<br>传入的第一个参数为args[6]



## 传递参数
参数后接冒号 可从外部传入参数；不接冒号意味着不需要指定值，返回true/false（命令行指定该参数意味着true）

    #!/bin/bash
    while getopts 'd:Dm:f:t:' OPT; do
        case $OPT in
            d)
                DEL_DAYS="$OPTARG";;
            D)
                DEL_ORIGINAL='yes';;
            f)
                DIR_FROM="$OPTARG";;
            m)
                MAILDIR_NAME="$OPTARG";;
            t)
                DIR_TO="$OPTARG";;
            ?)
                echo "Usage: `basename $0` [options] filename"
        esac
    done

## awk
awk导入外部变量

         awk -v i="$i" '$3==i 。。。。。
## 压缩 & 解压
tar -xf file.tar
tar -xzf file.tar.gz
tar -xjf file.tar.bz2
tar -xZf file.tar.Z
unrar e file.rar
unzip file.zip

tar -cf file.tar file
tar -czf file.tar.gz file
tar -cjf file.tar.bz2 file









## 问题
shell awk 浮点数比较出错问题


    
