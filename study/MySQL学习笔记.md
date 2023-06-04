# MySQL学习笔记

## 1.[数据库](https://blog.csdn.net/weixin_45851945/article/details/114287877?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167626667916800180679616%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167626667916800180679616&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-114287877-null-null.142^v73^insert_down2,201^v4^add_ask,239^v1^control&utm_term=mysql%20&spm=1018.2226.3001.4187)基本概念

访问数据库

`mysql -h 主机名 -P 端口号 -u 用户名 -p密码`

​      eg.`mysql -u root -p`

​			`mysql -u root -p123456`

改密码

`mysqladmin -u用户名 -p旧密码 password “新密码”`

​	eg`mysqladmin -uroot -p123 password '4GR56'`

`mysql -uroot -p456`

启动

`net start mysql80`

关闭

`net stop mysql80`

## 2.Mysql[数据库](https://www.bilibili.com/video/BV1j8411n7mS?p=3&vd_source=66be4fe8b4fb352044a1725fb9665060)管理操作

8.0以上版本要先`mysql -uroot -p123456`进入`mysql`

### 1.显示所有数据库

```sql
mysql> show databases;
```

### 2.创建数据库

```sql
mysql> create database 数据库名 charset-utf
8;   #解决中文乱码
mysql> create database 数据库名；
--查看创建的的数据库
show create database 数据库名;
```

### 3.删除数据库

```sql
mysql> drop database 数据库名；
```



### 4.选择数据库/查看当前选中的库

```sql
mysql> use db_name;   //使用某个数据库
mysql> select database();  //查看当前选中的数据库
```

### 5.显示数据库中的表

```sql
mysql> show tables;  //要先选中某个数据库use db_name;
```

## 3.建表操作

### 1.数据类型

#### 1.整数类型

![image-20230213190607129](D:\AppData\Typora\typora-user-images\image-20230213190607129.png)

#### 2.浮点数类型和定点数类型

MySQL数据库中使用浮点数和定点数来存储小数。浮点数的类型有两种：单精度浮点数类型（FLOAT)和双精度浮点数类型（DOUBLE)。而定点数类型只有一种即DECIMAL类型。下图列举了 MySQL中浮点数和定点数类型所对应的字节大小及其取值范围：![image-20230213190812427](D:\AppData\Typora\typora-user-images\image-20230213190812427.png)

从上图中可以看出：DECIMAL类型的取值范围与DOUBLE类型相同。但是，请注意：DECIMAL类型的有效取值范围是由M和D决定的。其中，M表示的是数据的长 度，D表示的是小数点后的长度。比如，将数据类型为DECIMAL(6,2)的数据6.5243 插人数据库后显示的结果为6.52

#### 3.字符串类型

在MySQL中常用CHAR 和 VARCHAR 表示字符串。两者不同的是：VARCHAR存储可变长度的字符串。
**当数据为CHAR(M)类型时，不管插入值的长度是实际是多少它所占用的存储空间都是M个字节；而VARCHAR(M)所对应的数据所占用的字节数为实际长度加1**

![image-20230213190932452](D:\AppData\Typora\typora-user-images\image-20230213190932452.png)

#### 4.文本类型

文本类型用于表示大文本数据，例如，文章内容、评论、详情等，它的类型分为如下4种：

![image-20230213191047575](D:\AppData\Typora\typora-user-images\image-20230213191047575.png)

#### 5.日期与时间类型



![image-20230213191138428](D:\AppData\Typora\typora-user-images\image-20230213191138428.png)

##### 1.YEAR类型

YEAR类型用于表示年份，在MySQL中，可以使用以下三种格式指定YEAR类型 的值。
1、使用4位字符串或数字表示，范围为’1901’—'2155’或1901—2155。例如，输人 ‘2019’或2019插人到数据库中的值均为2019。
2、使用两位字符串表示，范围为’00’—‘99’。其中，‘00’—'69’范围的值会被转换为 2000—2069范围的YEAR值，‘70’—'99’范围的值会被转换为1970—1999范围的YEAR 值。例如，输人’19’插人到数据库中的值为2019。
3、使用两位数字表示，范围为1—99。其中，1—69范围的值会被转换为2001— 2069范围的YEAR值，70—99范围的值会被转换为1970—1999范围的YEAR值。例 如，输人19插入到数据库中的值为2019。
请注意：**当使用YEAR类型时，一定要区分’0’和0。因为字符串格式的’0’表示的YEAR值是2000而数字格式的0表示的YEAR值是0000。**

##### 2. TIME类型

TIME类型用于表示时间值，它的显示形式一般为HH:MM:SS，其中，HH表示小时， MM表示分,SS表示秒。在MySQL中，可以使用以下3种格式指定TIME类型的值。
1、以’D HH:MM:SS’字符串格式表示。其中，D表示日可取0—34之间的值, 插人数据时，小时的值等于(DX24+HH)。例如，输入’2 11:30:50’插人数据库中的日期为59:30:50。
2、以’HHMMSS’字符串格式或者HHMMSS数字格式表示。 例如，输人’115454’或115454,插入数据库中的日期为11:54:54
3、使用CURRENT_TIME或NOW()输人当前系统时间。

##### 3. DATETIME类型

DATETIME类型用于表示日期和时间，它的显示形式为’YYYY-MM-DD HH: MM:SS’，其中，YYYY表示年，MM表示月，DD表示日，HH表示小时，MM表示分，SS 表示秒。在MySQL中，可以使用以下4种格式指定DATETIME类型的值。
以’YYYY-MM-DD HH:MM:SS’或者’YYYYMMDDHHMMSS’字符串格式表示的日期和时间，取值范围为’1000-01-01 00:00:00’—‘9999-12-3 23:59:59’。例如，输人’2019-01-22 09:01:23’或 ‘20140122_0_90123’插人数据库中的 DATETIME 值都为 2019-01-22 09:01:23。
1、以’YY-MM-DD HH:MM:SS’或者’YYMMDDHHMMSS’字符串格式表示的日期和时间，其中YY表示年，取值范围为’00’—‘99’。与DATE类型中的YY相同，‘00’— '69’范围的值会被转换为2000—2069范围的值，‘70’—'99’范围的值会被转换为1970—1999范围的值。
2、以YYYYMMDDHHMMSS或者YYMMDDHHMMSS数字格式表示的日期 和时间。例如，插入20190122090123或者190122090123,插人数据库中的DATETIME值都 为 2019-01-22 09:01:23。
3、使用NOW来输人当前系统的日期和时间。

##### 4. TIMESTAMP类型

TIMESTAMP类型用于表示日期和时间，它的显示形式与DATETIME相同但取值范围比DATETIME小。在此，介绍几种TIMESTAMP类型与DATATIME类型不同的形式：
1、使用CURRENT_TIMESTAMP输人系统当前日期和时间。
2、输人NULL时系统会输人系统当前日期和时间。
3、无任何输人时系统会输入系统当前日期和时间。

#### 6.二进制类型

在MySQL中常用BLOB存储二进制类型的数据，例如：图片、PDF文档等。

![image-20230213191609996](D:\AppData\Typora\typora-user-images\image-20230213191609996.png)

### 2.创建表

#### 1.建表

```sql
mysql> create table 表名（列名1 数据类型 约束
						 列名2 数据类型 约束
						 列名3 数据类型 约束...）;
		eg.create table stu(id int,
						 name varchar(20) );
```

#### 2.查看数据表

```sql
show tables;//查看当前数据库中所有表 
show create table student;//查表的基本信息 
desc student;//查看表的字段信息
```

#### 3.修改数据表

MySQL中使用`alter table`修改数据表

```sql
alter table student rename to stu;//表student改名为stu
alter table stu change name sname varchar(10);//修改字段名name=>sname
alter table stu modify sname int;//修改字段数据类型 varchar=>int
alter table stu add address varchar(50);增加字段addcess 
alter table stu drop address;//删除字段address

```

#### 4.删除表

```
drop table 表名;
```



### 3.简单约束

```sql
auto_increment 自动增长 由mysql自动维护 默认从1开始
primary key 主键 唯一标识数据库中的每条记录 不重复且非空 ~=unique + not null  格式：字段名 数据类型 primary key;
not null 非空，字段的值不能为空  格式：字段名 数据类型 NOT NULL;
unique 唯一可以为空
```

![image-20230213193128717](D:\AppData\Typora\typora-user-images\image-20230213193128717.png)

**主键约束**

方式一：

```sql
create table student(id int primary key,
		             name varchar(20));
```

方式二：

```sql
create table student01(id int name varchar(20),
					   primary key(id)      );
```

**默认值约束**

默认值约束即DEFAULT用于给数据表中的字段指定默认值

```sql
字段名 数据类型 DEFAULT 默认值；
eg.create table student03(id int,
						  name varchar(20),
						  gender varchar(10) default 'male');
```

**唯一性约束**

唯一性约束即UNIQUE用于保证数据表中字段的唯一性，即表中字段的**值**不能重复出现

```sql
字段名 数据类型 UNIQUE;
eg.create table student04(id int,
						  name varchar(20) unique);

```

### 4.数据表插入数据

```sql
示例：
mysql>DROP DATABASE IF EXISTS student;
mysql>create database student charset=utf8;
mysql>use student; 
mysql> create table student(id int,
					  name varchar(30),
        			  age int,
					  gender varchar(30) );
#查看表的结构
mysql>desc student;
#插入数据
##1为表中所有字段插入数据 INSERT INTO 表名（字段名1,字段名2,...) VALUES (值 1,值 2,...);
insert into student (id,name,age,gender) values (1,'bob',16,'male');
##2为表中指定字段插入数据 INSERT INTO 表名（字段名1,字段名2,...) VALUES (值 1,值 2,...);
##3同时插入多条记录      INSERT INTO 表名 [(字段名1,字段名2,...)]VALUES (值 1,值 2,…),(值 1,值 2,…),...;
insert into student (id,name,age,gender) values (2,'lucy',17,'female'),(3,'jack',19,'male'),(4,'tom',18,'male');
#查询数据
##查询所有列
select * from student; 
##查询指定列
select name,age from student;
```

### 5.可视化工具navicat

略

## 4.SQL查询语句

### 1.查询表中的列

1.查询所有列

```sql
select * from 表名;  
```

2.查询指定列

```
select 列名1，列名2.. from 表名;
```

### 2.列操作

1.列运算

```sql
select id+1,age*2 from student;
```

2.列拼接

```sql
select concat(age,'岁') from student;
```

3.列别名

```sql
select name as 姓名 from student;
select 列名 as 别名 from student；
注意：as可以省略
```

4.列去重

```sql
select distinct age from student;//把重复的值去掉
```

### 3.where子句

#### 1.条件查询

基本语法：

```sql
select ... from 表名 where 表达式；
```

eg.`select * from student where age>20;`

比较运算符:  > < =...

逻辑运算符: and or

范围: in(xx,xxx,...)   between .. and ..

```sql
select * from student where age>20 and id<4;
select id, name,age from student where id between 2 and 4;
select id, name,age from student where id in(1,2,3);
```

#### 2.空值判断

```sql
select ... from 表名 where 列名 is null;
select ... from 表名 where 列名 is not null;
```

#### 3.模糊查询

%：任意多个字符

_：一个字符

基本语法：

```sql
select ... from 表名 where 列名 like "%..%";
```

eg.

```sql
查询包含a的用户
select * from student where name like "%a%";//匹配任意个字符
查询a开头
select * from student where name like "a%";
查询a结尾
select * from student where name like "%a";
查询第二个字符为a的用户
select * from student where name like "_a%";
```

- like "%abc%" 含有abc
- like "%abc" 以abc结尾
- like "abc%" 以abc开头
- like "ab%_" 以ab开头，且ab后至少有一个字符
- like "%_%" 至少有两个字符 或者length(列名)> =2

#### 4.分页查询

limit m,n; //第一个数字表示起始的下标，第二个数字表示查询的条目

```sql
从第一条开始查询，共查询3条
select ... from 表名 limit 3；   //==limit 0,3
从第一条开始查询，共两条
select ... from 表名 limit 0,2；
从第三条开始查询，共3条
select ... from 表名 limit 2,3；
每页显示n条，查询第m页
select ... from 表名 limit (m-1)*n,n；
```

#### 5.order by:排序

语法：

```
select ... from 表名 order by 列名;
```

- ASC:升序（默认）小到大

- DESC：降序

  ```sql
  select * from student order by age;按年龄从小到大排序
  select * from student order by age，name;按年龄从小到大排序，如果年龄相同，按照姓名从小到大排序
  select * from student order by age desc;按年龄从大到小排序
  select * from student order by age desc，name;按年龄从大到小排序,如果年龄相同按姓名从小到大排列6.聚合函数
  ```

#### 6.聚合函数：组函数

- MAX()	最大值
- MIN()    最小值
- SUM()   求和
- AVG()    求平均值
- COUNT()   总数

#### 7.GROUD:分组统计

语法：

```sql
select ... from 表名 group by 列名
```

eg.

```sql
select max(id) from student group by age;  //以年龄分组，统计该组的最大id
```



## PyMySQL

- pymysql 模块基本架构：

```python
import pymysql
"创建数据连接实例"
"host:服务器/数据库主体地址和localhost同意=》本地地址"
"port:端口号 默认3306"
"user:连接用户名"
"password:连接密码"
my_connect = pymysql.Connect(
    host='127.0.0.1',
    port=3306,
    user='root',
    password='123456'
)
"创建游标：光标"
my_cur=my_connect.cursor()
"声明sql语句"
sql='use student;'
"声明触发器并执行sql语句"
my_cur.execute(sql)
"声明sql语句"
sql='select * from student;'
my_cur.execute(sql)
"返回结果"
"fetchall():返回所有结果"
res=my_cur.fetchall()
print(res)
"fetchone():返回首行结果"
"为什么结果是None?pymysql是一个中间件 python从中间件中读取输入"
res=my_cur.fetchone()
print(res)
#增
sql='insert into student values(6,"cao",25,"男");'
my_cur.execute(sql)
"commit():提交到数据库"
my_connect.commit()

my_cur.close()	#先关闭cursor
my_connect.close()	#后关闭connect
```

### 1.获取连接

```python
import pymysql
"创建数据连接实例"
"host:服务器/数据库主体地址和localhost同意=》本地地址"
"port:端口号 默认3306"
"user:连接用户名"
"password:连接密码"
"db:使用的库名"
"charset:连接时使用的字符串"
my_connect = pymysql.Connect(
    host='127.0.0.1',
    port=3306,
    user='root',
    password='123456'
    db="student",
    charset='utf8'
)
```

### 2.获得Cursor对象

```python
"创建游标：光标"
my_cur=my_connect.cursor()
```

### 3.执行SQL

```python
#执行查询，返回查询出有多少行
row_count=my_cur.execute("select id,name,age from student where id>5")
<=>
id=5
row_count=my_cur.execute("select id,name,age from student where id>" + str(id))
<=>
id=5
row_count=my_cur.execute("select id,name,age from student where id> %d" %id )


#执行增删改，返回影响的行数
sql="insert into student(name,age,gender)values(6,"cao",25,"男");"
row_count=my_cur.execute(sql)
```

注意：执行增删改操作时，需要使用`connect.commit()`提交到数据库：

```python
my_cur.execute(...)
my_connect.commit()
```

### 4.执行查询

```python
row_count=my_cur.execute("查询的sql语句")  #返回查询到的数据行数，没有数据返回0
my_cur.fetchone()	#获取查询到的1条数据
my_cur.fetchmany(3)	#获取查询到的3条数据
my_cur.fetchall()	#获取所有数据
```

- cursor中是所有查到的数据，从中获取数据，需要向下移动游标，游标起始位置是第一行数据上一行

- fetchone()游标下移一行，获取一行数据(tuple),如果没有数据返回None

- fetchmany(n)游标下移n行，获取n行数据(tuple of tuple),如果没有数据返回空tuple:()

- fetchall()游标移动到底，获取所有数据行(tuple of tuple),如果没有数据返回空tuple:()

技巧：*有值/None*     *非空tuple/空tuple*     可以作为True/False使用，判断是否查询到了数据.
从cursor中获取的每一行数据的格式为一个tuple,其中是各列的值 EG.(6,"cao",25,"男")
数据表中的列类型和python类型的对应为：
	int/double/float =int/float
	varchar/char =str
	decimal =decimal.Decimal
	datetime =datetime.datetime

### 5.执行增删改

```python
count=my_cur.execute("执行增删改的语句")  #返回影响的行数
```

执行增删改需要控制事务，提交或者回滚事务

```
my_cur.commit()		#提交
my_cur.rollback()	#回滚	
```

### 6.资源回收

```python
my_cur.close()	#先关闭cursor
my_connect.close()	#后关闭connect
```

### 7.cursor类型选择

```python
#tuple
my_cur=my_connect.cursor()
row_count=my_cur.execute('select * from student;')
res=my_cur.fetchall()
for t in result:
    print(t[1])
    
#res=my_cur.fetchall()结果：
((1, 'bob', 16, 'male'), (2, 'lucy', 17, 'female'), (3, 'jack', 19, 'male'), (4, 'tom', 18, 'male'), (5, 'linda', 22, '女'), (6, 'cao', 25, '男'))    
    
#dict    
my_cur=my_connect.cursor(MySQLdb.cursors.DicCursor)		#选择了cursor类型
my_cur.execute('select * from student;')
my_cur.fetchone()	#此时fetchone()返回的不再是tuple,而是一个dict，key是列名，value是列值
my_cur.fetchall()/fetchmany()	#返回tuple of dict,每一个dict是一行数据 

#res=my_cur.fetchall()结果：
[{'id': 1, 'name': 'bob', 'age': 16, 'gender': 'male'}, {'id': 2, 'name': 'lucy', 'age': 17, 'gender': 'female'}, {'id': 3, 'name': 'jack', 'age': 19, 'gender': 'male'}, {'id': 4, 'name': 'tom', 'age': 18, 'gender': 'male'}, {'id': 5, 'name': 'linda', 'age': 22, 'gender': '女'}, {'id': 6, 'name': 'cao', 'age': 25, 'gender': '男'}]

```

### 总结：

Python操作Mysql的步骤：
(1) 连接mysql 	`my_connect=pymysql.connect(xxx)`

(2) 获取游标对象	`my_cur=my_connect.cursor(游标的类型)`

(3) 执行SQL指令-指令可以是增删改查`cursor..execute("SQL语句")`
(4) 根据SQL指令的不同，需要做不同的操作

如果是查询指令：`my_cur.fetchone/fetchmany/fetchall`
如果是增删改指令：`my_connect.commit()`

(5) 释放资源：关闭curse和conn

补充：

```python
col=[i[0] for i in my_cur.description]   #获取字段名列表
结果：['id', 'name', 'age', 'gender']

#输出为excel格式
def export_excel(table_name):
    """
    table_name: 数据库中的表名
    """
    # 连接数据库，查询数据
    host, user, passwd, db = 'localhost', 'user1', 'cxh12345', 'qiaodao'
    conn = pymysql.connect(user=user, host=host, port=3306, passwd=passwd, db=db, charset='utf8')
    cur = conn.cursor()
    sql = 'select * from %s' % table_name
    cur.execute(sql)  # 返回受影响的行数

    fields = [field[0] for field in cur.description]  # 获取所有字段名
    all_data = cur.fetchall()  # 所有数据

    # 写入excel
    book = xlwt.Workbook()
    sheet = book.add_sheet('sheet1')

    for col, field in enumerate(fields):
        sheet.write(0, col, field)

    row = 1
    for data in all_data:
        for col, field in enumerate(data):
            sheet.write(row, col, field)
        row += 1
    book.save("%s.xls" % table_name)
if __name__ == '__main__':
     export_excel('tab_user')
法二：       
def creat_ex():
    conn = pymysql.connect(host='10.133.77.108',user='user1',password='cxh12345',db='qiaodao',charset='utf8')
    cursor = conn.cursor()

    count = cursor.execute('select * from qd')

    # 重置游标的位置
    cursor.scroll(0,mode='absolute')
    # 搜取所有结果
    results = cursor.fetchall()

    # 获取MYSQL里面的数据字段名称
    fields = cursor.description
    workbook = xlwt.Workbook()
    sheet = workbook.add_sheet('qd',cell_overwrite_ok=True)

    # 写上字段信息
    for field in range(0,len(fields)):
        sheet.write(0,field,fields[field][0])

    # 获取并写入数据段信息
    row = 1
    col = 0
    for row in range(1,len(results)+1):
     for col in range(0,len(fields)):
            sheet.write(row,col,u'%s'%results[row-1][col])
    time1 = datetime.now()
    path = f'{time1.year}-{time1.month}-{time1.day}'
    workbook.save(r'./qiandao.xls')
```

