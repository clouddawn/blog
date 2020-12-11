# 命令行基础（一）

## pwd

* 查看当前完整路径

![image](../images2/56/1.png)(1)

## touch

* 创建文件 

touch test1.html


* 创建多个文件 

touch test1.css test1.js

## echo

* 显示字符串

![image](../images2/56/4.png)(4)

* echo 'Hello World' > test1.txt  
在txt文件里写入字符串 

* echo $PATH   
展示环境变量

![image](../images2/56/6.png)(6)


## ls

* 列出当前目录下的文件夹

![image](../images2/56/7.png)(7)

* ls -a   
列出所有文件，包含隐藏文件

![image](../images2/56/8.png)(8)

* ls -al   
列出所有文件，包含隐藏文件，文件显示详细信息

![image](../images2/56/9.png)(9)

# mkdir

mkdir test1   
在当前目录下创建test1文件夹

# rm 

删除文件或文件夹

* rm 文件路径  
删除文件  


* rm -r 目录路径  
删除目录，递归处理，将指定目录（文件夹）下的所有文件与子目录一并处理

* rm -rf 目录路径  
强制删除目录，无法恢复


命令行释义查询：[explainshell.com](https://explainshell.com)




