# shell
## 1.权限设置
umask 022 设置新建文件或目录的权限，新文件权限为（666-022=644），新目录的权限为（777-022=755）
<br>修改文件权限 chmod 755 file 
<br>修改文件属主 chown  wxm test.txt  
<br>修改文件所属组 chgrp  group1 text.txt 
<br>修改用户所属组 usermod -G manage wxm 会保留原来所在的组
<br>查看用户所在组 groups wxm
## 2.变量赋值
a=aa
<br>b=bb
<br>echo $a 
## 3.字符串拼接
c=${a}_vs_${b}
<br>打印输出结果为a_vs_b
## 4.字符串拆分
<br>i=WB_vs_WP
<br>echo $i | sed 's/_vs_/\t/g' | cut -f 1
## 5.调用R脚本
cat test.R | R --vanilla --slave --args <参数1>
<br>传入的第一个参数为args[5]
<br>Rscript test.R <参数1>
<br>传入的第一个参数为args[6]



## 6.传递参数
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
## 7.压缩 & 解压
* 解压
tar -xf file.tar
<br>tar -xzf file.tar.gz
<br>tar -xjf file.tar.bz2
<br>tar -xZf file.tar.Z
<br>unrar e file.rar
<br>unzip file.zip
<br>gunzip file.gz
* 压缩
<br>tar -cf file.tar file
<br>tar -czf file.tar.gz file
<br>tar -cjf file.tar.bz2 file
<br>gzip file

## 8.修改打开文件上限
针对exhaust open files limit报错
* 默认状态
    
        $ ulimit -Hn
        4096
        $ ulimit -Sn
        1024
* 做出修改 

        vim /etc/security/limits.conf
        增加如下内容
        * soft nproc 655350
        * hard nproc 655350
        * soft nofile 655350
        * hard nofile 655350
* 修改后结果

        $ ulimit -Hn
        655350
        $ ulimit -Sn
        655350

##报错
sed替换报错

        sed: -e expression #1, char 15: unknown option to `s'

原因是所替换目标中有/
<br>可将sed "///" 改为 sed "@@@"



## 问题
shell awk 浮点数比较出错问题

## 9.查看目录或文件占用大小
* 查看当前目录占用大小

    du -h --max-depth 0 ./
    #0为当前目录，数字代表当前目录层数

## 修改环境变量

    /etc/profile
    
## time命令

* 在交互界面调用方式 /usr/bin/time 
* 脚本中可直接time调用
* 结果输出重定向 2>

## for 循环
* 遍历数字序列

        for i in $(seq 1 5 20) #从1开始，步长5，小于等于20的值
        for i in {1..10} #从1开始，步长1，小于等于10的值
        for ((i=0;i<10;i++)) #从0开始，步长1，小于10的值
        for ((i=0;i<10;i+=2)) #从0开始，步长2，小于10的值
* 遍历序列终点值由变量传入

        END=5
        for i in `seq 1 $END`
        for i in `eval echo {1..$END}`
        for ((i=0;i<$END;i++))

## 查看进程占用磁盘I/O

    pidstat -d 1
