尝试在Github创建个人博客便于记录自己编程学习过程
#Python学习第1天

##1. 列表（list）
append 添加元素
remove 删除元素
（关于以上‘方法’，是可以改变列表的）
len函数：查看列表元素数量
max函数/min函数：求最大/最小值
sorted函数：排序

关于查询
列表第一个元素是0

##2. 字典/通讯录（dict）
del 字典名 [ ] ：删除键和值
键 in 字典名：查询该键是否存在于该字典

#Python学习第2天
round函数：小数点后几位
.split（）：在括号内输入想要分隔的符号，如下划线，可将字符串分割成一个列表

##3.循环
for 变量 in 序列：对于序列中的每个元素，进行操作
range（3）：表示范围，生成0，1，2（左闭右开原则），常配合len函数在for循环中使用，例如 for i in range(len(变量))
extend：并集，将一个列表追加在一个列表的后面，例如 history.extend(list)，把list追加在history后面

##如何在python中读取txt文件？