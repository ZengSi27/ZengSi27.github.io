尝试在Github创建个人博客便于记录自己编程学习过程
# Python学习第1天

## 1. 列表（list）
append 添加元素
remove 删除元素
（关于以上‘方法’，是可以改变列表的）
len函数：查看列表元素数量
max函数/min函数：求最大/最小值
sorted函数：排序

关于查询
列表第一个元素是0

## 2. 字典/通讯录（dict）
del 字典名 [ ] ：删除键和值
键 in 字典名：查询该键是否存在于该字典

# Python学习第2天
round函数：小数点后几位
.split（）：在括号内输入想要分隔的符号，如下划线，可将字符串分割成一个列表

## 3.循环
for 变量 in 序列：对于序列中的每个元素，进行操作
range（3）：表示范围，生成0，1，2（左闭右开原则），常配合len函数在for循环中使用，例如 for i in range(len(变量))
extend：并集，将一个列表追加在一个列表的后面，例如 history.extend(list)，把list追加在history后面
if函数：可以用于筛选满足特定条件的元素，例如选出ROI大于1的月份

## 如何在python中读取txt文件？

- open(路径，模式，encoding="utf-8")，模式：w（只读）、r（只写）

read方法：用于读取txt，大文件不要用，占用过多内存。read之后记得close
补充：read（数字），读取多少字节；readline（）读取行；readlines读取所有行

- with open(路径) as f：无需close来结束调用，节约内存 

## 4.自定义函数

- def：根据需求，确定有无参数，有无返回值（return）

# Python学习第3天——Pandas

## 1.如何读取数据
csv/tsv/txt、excel、mysql三种文件方法不同

- 1.1 csv
fpath = "路径"
pd.read_csv(fpath) 读取数据
.head() 查看前几行
.shape 查看形状（行数、列数）
.columns 查看列名列表
.index 查看索引列
.dtypes 查看数据类型
- 1.2 excel
pd.read_excel(fpath)
- 1.3 mysql
pd.read_sql("", )

## 2.数据结构（Series和Dataframe）
Series:一维数据，一行或一列，可以理解为字典
DataFrame:二维数据，有行有列，可以理解为excel

## 3.查询数据
- 3.1 df.loc查询数据的方法
1.使用单个label值查询
2.使用值列表批量查询
3.使用区间[:]范围查询
补充：df.loc[1,3] 查询行，包括3（与python不同）
4.使用条件表达式查询
5.调用函数查询

