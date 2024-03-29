[创建新用户(添加root权限)](https://blog.csdn.net/weixin_44569100/article/details/98749869?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168378809416800215010088%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=168378809416800215010088&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-9-98749869-null-null.142^v86^insert_down1,239^v2^insert_chatgpt&utm_term=ubuntu%E5%88%9B%E5%BB%BA%E6%96%B0%E7%94%A8%E6%88%B7&spm=1018.2226.3001.4187)

[修改用户名和用户密码](https://blog.csdn.net/m0_54647521/article/details/127521032)

[ssh远程连接](https://www.bilibili.com/video/BV1gt411L7me/?spm_id_from=333.337.search-card.all.click&vd_source=66be4fe8b4fb352044a1725fb9665060)

`ssh czh@192.168.5.152`

[vscode ssh远程连接](https://www.bilibili.com/video/BV15D4y177Ko/?spm_id_from=333.880.my_history.page.click&vd_source=66be4fe8b4fb352044a1725fb9665060)

[vim编辑指令](https://blog.csdn.net/weixin_39653948/article/details/116352298)

编辑模式 `i`

退出：

1.保存并退出：    按下 `ESC` 之后，输入 `: + w + q`

2.不保存并退出：按下 `ESC` 之后，输入 `: +q+!`

# linux常用命令：

ls 相关常用命令:
1.`ls` 或者 `l` 显示当前文件夹下的文件信息
2.`ls -a` 显示所有文件, 包括以 "."开头的隐藏文件
3.`ls -l` 显示详细信息  `ls -lh`加-h参数可以人性化显示文件大小
4.`ll` 或 `ls -al` 显示所有文件，包括隐藏文件的详细信息

5.`ll w.txt a.txt`显示特定文件或者文件夹

![image-20230505142614091](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202306041624151.png)

cd 相关常用命令:
`cd 目录名` 切换到对应目录下
`cd ..` 或者 `cd ../` 切换到上级目录
`cd -` 切换到上次浏览的目录并打印当前工作目录路径
`cd /` 切换到根目录

pwd 相关常用命令:
`pwd` 打印当前工作目录路径

touch 相关常用命令:
`touch 文件名` 修改文件时间属性，若文件名不存在，则新建一个新的同名文件

cp 相关常用命令:
`cp 文件或者目录` 主要用于复制文件或目录
`cp -p` 保留源文件或目录的属性
`cp -r` 复制目录及目录内的所有内容

`cp -rp`复制目录及目录内的所有内容,保留源文件或目录的属性

`cp -v` 显示命令执行的过程

mv 相关常用命令:
`mv 源文件或目录 目标文件或目录` 移动或重命名文件或目录

mkdir 相关常用命令:
`mkdir 目录名` 新建一个不存在的目录，mkdir 是“make directory”的缩写词
`mkdir -p` 确保目录名称存在，不存在的就新建一个
`mkdir -v` 显示命令执行的过程

rmdir 相关常用命令:
`rmdir 目录名` 删除空目录，rmdir 是“remove directory”的缩写词
`rmdir -p` 删除指定目录后，若该目录的上一级目录已变成空目录，则将其一并删除
`rmdir -v` 显示命令执行的过程

rm 相关常用命令:
`rm 文件名或目录名` 删除一个文件或者目录，rm 是“remove”的缩写词
`rm -r` 强制删除目录及目录下的所有文件
`rm -i` 删除前逐一询问确认
`rm -v` 显示命令执行的过程

locate 相关常用命令:
`locate 要搜索的文件或目录名` 非实时的从数据库里快速搜索文件或目录

> 若需要更新数据库，可以使用命令`updatedb`

`locate -V` 显示命令的版本信息

man 相关常用命令:
`man 命令名` 可以查看命令的帮助信息

help 相关常用命令:
`help 命令名` 可以查看命令的帮助信息

chmod 相关常用命令:
`chmod 文件或目录名` 修改文件或目录的权限信息

用法: `chmod   [u|g|o|a]   [=|+|-]   [r|w|x]`   文件名

![8](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202306041631864.png)

r = 4 = 读取属性
w = 2 = 写入属性
x = 1 = 执行属性

-无

![image-20230505150308099](https://cdn.jsdelivr.net/gh/caozihao1205/blog_img/img/202306041624152.png)

**VSCode : vscode-remote下无法写入文件及linux文件读写权限**

比如，当前是**songroom用户**，需要**改变wasm_test的权限**，可以

```bash
sudo chown -R songroom wasm_test
```

具体模式是：

```bash
sudo chown -R $USER <directory_project>
```

要**修改文件夹内所有的文件和文件夹及子文件夹属性为可写可读可执行**，比如rust_test

```bash
chmod -R 777 /upload

songroom@DESKTOP-MEDPUTU:~/rust_test$ sudo chmod -R 777  ~/rust_test
```

**查看文件大小：**

ls 命令一般用于查看文件和目录的信息，包括文件和目录权限、拥有者、所对应的组、文件大小、修改时间、文件对应的路径等等信息

`ls -lh path`

查询当前目录下所有子目录总大小 并按大小排序

`du -sh * | sort -nr` 

查询当前目录下所有子目录总大小 , * 指所有目录，如果只要查询某个目录 替换掉*即可

`du -sh *`

查询path目录下所有子目录总大小

`du -sh path/*`

列出path目录下文件（文件夹）的大小

`du -sh path`

查询当前目录下各级目录大小

`du -h path`

- Ubuntu系统中的wget命令 [here](https://blog.csdn.net/weixin_43786241/article/details/105559712?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168664146016800180628677%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=168664146016800180628677&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-105559712-null-null.142^v88^control,239^v2^insert_chatgpt&utm_term=ubuntu%20wget&spm=1018.2226.3001.4187)

最基础：`wget  https://github.com/fchollet/deep-learning-models/releases/download/v0.7/inception_resnet_v2_weights_tf_dim_ordering_tf_kernels_notop.h5`

上述从网络下载一个文件并保存在当前目录，在下载的过程中会显示进度条，包含（下载完成百分比，已经下载的字节，当前下载速度，剩余下载时间）。

- tar命令：Linux下的解压与压缩命令 [here](https://blog.csdn.net/oqqHuTu12345678/article/details/70162387?ops_request_misc=&request_id=&biz_id=102&utm_term=tar&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-9-70162387.142^v88^control,239^v2^insert_chatgpt&spm=1018.2226.3001.4187)
