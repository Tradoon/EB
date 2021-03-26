linux备忘录

man 手册

```注释
查看man文档

         man          章节号     命令

例如：我想查看ls的man手册第5章节的内容：man   5  ls

 Man手册说明：

         NAME：名字，功能性说明

         SYNOPSIS:详细功能描述

         DESCRIPTION:命令功能的详尽说明，可能包括每一项的意义

         AUTHOR:作者

         COPYRIGHT:版本信息

         SEE ALSO:其他相关信息

         OPTIONS:选项，说明每一个选项的意义

         FILES:此命令的相关配置文件

Man相关快捷键：

         翻页：

空格键或Ctrl+f：向下翻一屏

                  Ctrl+b：向上翻一屏

                  Ctrl+d：向下翻半屏

                  Ctrl+u：向上翻半屏

                  回车键：向下翻一行

                  k：向上翻一行

                  j：向下翻一行

                  g或者1G：首行

                  G：最后一行

                   q：退出

         查找：

                   /keyword：自上往下查找

                   /keyword：自下往上查找

                   n：下一个匹配

                   N：上一个匹配
```

查看目录中文件所有者

```shell
ls -l  file
ll file
```



![image-20210322090132049](C:\Users\tradoon\AppData\Roaming\Typora\typora-user-images\image-20210322090132049.png)

![image-20210322090421389](C:\Users\tradoon\AppData\Roaming\Typora\typora-user-images\image-20210322090421389.png)



![image-20210322091924360](C:\Users\tradoon\AppData\Roaming\Typora\typora-user-images\image-20210322091924360.png)

![image-20210322093257364](C:\Users\tradoon\AppData\Roaming\Typora\typora-user-images\image-20210322093257364.png)

![image-20210322093310756](C:\Users\tradoon\AppData\Roaming\Typora\typora-user-images\image-20210322093310756.png)

1显示分组

2 增加用户所属的分组

![image-20210322093849651](C:\Users\tradoon\AppData\Roaming\Typora\typora-user-images\image-20210322093849651.png)

```linux
cat /etc/group | sort
查看结果按字典排序
cat /etc/group | grep -E "shiyanlou"
筛选含有实验楼字段的
```

改变文件所有者

```python
chown user file
```



shell 变量

声明

+ declare 声明之后进行赋值
+ 不需要声明直接赋值

```shell
#1
declare tmp
tmp=hello
#2
tmp=hello

```

输出变量

echo 就相当于printf

```shell
echo $tmp
```

![image-20210323104155666](C:\Users\tradoon\AppData\Roaming\Typora\typora-user-images\image-20210323104155666.png)

如果是echo tmp就输出这个变量本身，而非变量内包含的内容

查看当前系统安装的shell



```shell
cat /etc/shells
```

![image-20210323150620701](C:\Users\tradoon\AppData\Roaming\Typora\typora-user-images\image-20210323150620701.png)



**shell变量的类型**

+ 当前shell用户自定义的变量，是shell进程私有的变量，只在当前shell中有效
+ shell本身内建的变量
+ 自定义变量导出的环境变量



打印环境变量

![image-20210323104747188](C:\Users\tradoon\AppData\Roaming\Typora\typora-user-images\image-20210323104747188.png)

环境变量

  我认为

 在shell进程和其子进程都能够使用的变量就是环境变量（有点类似全局变量）

+ 临时环境变量 

  + 在shell及其子进程执行过程中存在并起作用，进程结束，该环境变量生存周期结束（直接使用export就可以）

    

+ 更改文件配置

  + /etc/profile中保存对所有用户生效的环境配置
  + /etc/bashrc 保存shell变量
  + 每个用户的/home/.profile文件中的环境变量只对当前用户永久生效

```shell
tmp=shiyanlou
echo $tmp
#output：shiyanlou
zsh 
echo $tmp
#output:无
exit
export tmp
zsh
echo $tmp
#output:shiyanlou
```

`  >>追加方式加入到文件中

`  >覆盖方式加入到文件中

![image-20210323145939545](C:\Users\tradoon\AppData\Roaming\Typora\typora-user-images\image-20210323145939545.png)

unset 可以删除普通变量或者是环境变量



让环境变量生效

+ 重启
+ ```source .zshrc```
+  ```. ./.zshrc```  .是source的别名，但是后面必须指明zshrc的相对或者绝对路径，source不需要（zsh是因为使用的shell是zsh）

**搜索**

| which                                                        | whereis                                                  | find                                       | locate                                                     |
| ------------------------------------------------------------ | -------------------------------------------------------- | ------------------------------------------ | ---------------------------------------------------------- |
| 搜索以确定是否安装了某个指定的程序                           | 只能搜索二进制文件（-b)，man帮助文件(-m)和源代码文件(-s) | 可以通过文件类型，文件名，文件属性进行搜索 | 查找指定目录下不同文件类型，支持递归查询，**指定类型查找** |
| 从PATH环境变量指定的路径中去搜索命令并且返回第一个搜索到的结果 | 不遍历硬盘，通过数据库查询                               | 不知道                                     | 不遍历硬盘，通过查询特定数据库来检索信息                   |
|                                                              |                                                          |                                            |                                                            |

查找详细信息：https://www.lanqiao.cn/courses/1/learning/?id=60

zip使用：

https://www.lanqiao.cn/courses/1/learning/?id=61

打包压缩

zip

| 安静模式 | 递归 | 输出为 | 创建加密压缩包 |
| -------- | ---- | ------ | -------------- |
| -q       | -r   | -o     | -e             |

有1-9的压缩级别 （-9表示用第九级别压缩）

解压

unzip

| 安静模式 | 不解压仅查看压缩包内容 | 指定编码类型 | 解压到指定目录 |
| -------- | ---------------------- | ------------ | -------------- |
| -q       | -l                     | -0           | -d             |



tar

| 创建一个tar包文件 | -v       | -f             |
| ----------------- | -------- | -------------- |
| -c                | 可视方式 | 执行创建文件名 |

解压

| 解压一个文件 | 不解压仅查看压缩包内容 | 解压到已存在的目录 |      |
| ------------ | ---------------------- | ------------------ | ---- |
| -x           | -t                     | -C                 |      |

tar 常用压缩格式

```shell
tar -czf shiyanlou.tar.gz /home
#使用z参数，使用gzip工具创建*.tar.gz

tar -xzf shiyanlou.tar.gz
#解压
```

不同格式对应的参数

![image-20210325090131211](F:\big-three\review\eb\image-20210325090131211.png)



看不懂：

https://www.lanqiao.cn/courses/1/learning/?id=62

