# Linux_Commands

简要汇总一些 Git 教程中经常遇到的 Linux 命令，这里只给出常见用法，并不会全面讲解。

**cat**：连接文件并打印到标准输出设备上，也用于创建文件。

```
# 设ml和m2是当前目录下的两个文件
cat m1 （在屏幕上显示文件ml的内容）
cat m1 m2 （同时显示文件ml和m2的内容）
cat m1 m2 > file （将文件ml和m2合并后放入文件file中）
cat > filename (创建一个文件)
```

**cd**：切换工作目录至 [dirname](http://man.linuxde.net/dirname)。 其中 dirName 表示法可为绝对路径或相对路径。若目录名称省略或为 `~` ，则变换至使用者的 home directory (也就是刚[login](http://man.linuxde.net/login)时所在的目录)。`.` 则是表示目前所在的目录，`..` 则表示目前目录位置的上一层目录。

```
cd    进入用户主目录；
cd ~  进入用户主目录；
cd -  返回进入此目录之前所在的目录；
cd ..  返回上级目录（若当前目录为“/“，则执行完后还在“/"；".."为上级目录的意思）；
cd ../..  返回上两级目录；
cd !$  把上个命令的参数作为cd参数使用。
```

**echo**：在标准输出上显示字符串，或是将字符串定向输出到文件中

```
echo "It is a test" > myfile
```

**ls**：列出目录下的文件 (默认是当前目录)， [URL](https://www.cnblogs.com/ginvip/p/6351696.html) 。

**ll**：“ll”是“ls -l"的别名，显示当前目录下文件的详细信息。

**mkdir**： 创建目录

**pwd**：显示当前所在工作目录的全路径， [URL](http://blog.csdn.net/gnail_oug/article/details/70664458) 

**rm**：删除文件或文件夹

**touch**：创建二进制文件，

**vi/vim**：进入 vim 编辑器，vi+文件名也可创建文件