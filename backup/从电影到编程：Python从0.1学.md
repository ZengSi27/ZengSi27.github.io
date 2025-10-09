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

## 1.如何读取和导出数据
csv/tsv/txt、excel、mysql三种文件读取方法不同
- 1.1 csv
fpath =( "路径") 
同一文件夹下直接输入文件名即可读取

pd.read_csv(fpath) 读取数据
, converters={'uid' : str}加在fpath后面可以把uid这列按照“字符串”类型读取
另一种方式是用 .astype(str) 方法

.head() 查看前几行
.shape 查看形状（行数、列数）
.columns 查看列名列表
.index 查看索引列
.dtypes 查看数据类型
- 1.2 excel
pd.read_excel(fpath)
- 1.3 mysql
pd.read_sql("", )

- 1.4导出数据
.to_excel('test excel.xlsx', index = False)导出到同一文件夹下，index = False 是删除第一列索引列

## 2.数据结构（Series和Dataframe）
Series:一维数据，一行或一列，可以理解为字典
DataFrame:二维数据，有行有列，可以理解为excel

## 3.查询数据
excel['id']查询id这一列的数据，类似python字典
excel.iloc[1]查询第二行数据

- 3.1 df.loc查询数据的方法
1.使用单个label值查询
2.使用值列表批量查询
3.使用区间[:]范围查询
补充：df.loc[1,3] 查询行，包括3（与python不同）
4.使用条件表达式查询（布尔索引）
excel[excel['progress']>= 100000 ]会返回一个符合条件的dataframe
5.调用函数查询

- 数据筛选的补充
excel.drop_duplicates(subset='uid', keep = 'last', inplace = True )删除重复值
subset='uid' 删除uid这列的重复的值
keep = 'last' 仅保留最后一个值
 inplace = True 替换整个列表，false的话是不替换仅展示

# Python学习第4天
## 1.轴、合并与连接
1.1关于轴：
Columns（列，axis=1）自左向右
Index（行，axis=0）自上向下

1.2关于合并与连接
pd.concat([excel, excel2], axis = 0) 两个表合并，按照自上而下的方向
pd.merge(excel, excel2, how = 'inner', on = 'uid') 两个表合并
on: 左右都需要有这个key
left_on: 左边的key
right_on: 右边的key

参考视频课程链接：https://www.bilibili.com/video/BV1UJ411A7Fs?spm_id_from=333.788.videopod.episodes&vd_source=12234dcd5ca10446ab2cc18135e10a62&p=13


#SQL从0开始
##1、select和from
语法结构：select--from--where--group by--having--order by--limit
运行顺序：from--where--group by--having--order by--limit--select（弟中弟）

##2、where
用于限定from的对象，可用数学运算和逻辑运算符号（需要注意in的用法）

模糊查询：
第一种是 like 'C%ia' 寻找C字母开头，ia字母结尾的国家名称
第二种是占位符 like '_t%' 查询国家名中第二个字符为't'的国家

例题：查询既包含有所有元音字母（a,e,i,o,u），同时国家名中没有空格的国家，最后显示他们的名字
我的答案：
`select name 国家
from world
where name like '%a%'
and name like '%e%'
and name like '%i%'
and name like '%o%'
and name like '%u%'
and name not like '% %'`
可以简化为？这里怎么简化呢

##3、order by排序
默认升序（从小到大）

例题：查询1984年所有获奖者的姓名和奖项科目。结果将诺贝尔化学奖和物理学奖排在最后，然后按照科目排序，再按照获奖者姓名排序
我的答案：
`select
winner
,subject
from nobel
where yr = 1984
order by subject in ('chemistry','physics') , subject, winner` 这里的in的使用，让后面两个科目返回的值为1，默认排在0后面

##4、limit

##5、聚合函数和group by
例题：查询2013至2015年每年每个科目的获奖人数，结果按年份从大到小，人数从大到小排序
我的答案：
select yr, subject, count(winner) 获奖人数
from nobel
where yr between 2013 and 2015
group by yr,subject
order by yr desc,count(winner) desc

##6、having和简单运行原理
having是聚合后筛选，where是聚合前筛选

例题：查询总人口数至少为3亿的大洲和其平均gdp，其中只有gdp高于200亿且人口数大于6000万或者gdp低于80亿且首都中含有三个a的国家的计入计算，最后按国家数从大到小排序，只显示第一行
`select continent, avg(gdp) 平均GDP
from world
where gdp>=20000000000 and population>=60000000
or gdp<8000000000 and name like '%a%a%a%'
group by continent
having sum(population)>=300000000
order by count(name) desc
limit 1`

##7、其他常见函数
round(x,y)——四舍五入
concat(s1,s2,...)——连接字符串函数
