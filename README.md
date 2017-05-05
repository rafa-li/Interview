# Interview
##数据库方面：
####数据表常用操作：
- 1.增  
1.1【插入单行】  
insert [into] <表名> (列名) values (列值)
<pre>
例：insert into Strdents (姓名,性别,出生日期) values
</pre>
1.2【将现有表数据添加到一个已有表】  
insert into <已有的新表> (列名) select <原表列名> from <原表名>
<pre>
例：insert into tongxunlu ('姓名','地址','电子邮件')
select name,address,email
from Strdents
</pre>
1.3【直接拿现有表数据创建一个新表并填充】  
select <新建表列名> into <新建表名> from <源表名>
<pre>
例：select name,address,email into tongxunlu from strdents
</pre>
1.4【使用union关键字合并数据进行插入多行】  
insert <表名> <列名> select <列值> tnion select <列值>
<pre>
例：insert Students (姓名,性别,出生日期)
select '开心朋朋','男','1980/6/15' union（union表示下一行）
select '蓝色小明','男','19\**/\*\*/\*\*'
</pre>

- 2.删  
2.1【删除<满足条件的>行】  
delete from <表名> [where <删除条件>]
<pre>
例：delete from a where name='开心朋朋'（删除表a中列值为开心朋朋的行）
</pre>
2.2【删除整个表】  
truncate table <表名>
<pre>
例：truncate table tongxunlu
</pre>
注意：删除表的所有行，但表的结构、列、约束、索引等不会被删除；不能用语有外建约束引用的表

- 3.改  
update <表名> set <列名=更新值> [where <更新条件>]
<pre>
例：update tongxunlu set 年龄=18 where 姓名='蓝色小名'
</pre>

- 4.查  
4.1``精确（条件）查询
<pre>
select <列名> from <表名> [where <查询条件表达试>] [order by <排序的列名>[asc或desc]]
</pre>
4.1.1【查询所有数据行和列】
<pre>
例：select * from a
说明：查询a表中所有行和列
</pre>
4.1.2【查询部分行列--条件查询】
<pre>
例：select i,j,k from a where f=5
说明：查询表a中f=5的所有行，并显示i,j,k３列
</pre>
4.1.3【在查询中使用ＡＳ更改列名】
<pre>
例：select name as 姓名 from a where xingbie='男'
说明：查询a表中性别为男的所有行，显示name列，并将name列改名为（姓名）显示
</pre>
4.1.4【查询空行】
<pre>
例：select name from a where email is null
说明：查询表a中email为空的所有行，并显示name列；SQL语句中用is null或者is not null来判断是否为空行
</pre>
4.1.5【在查询中使用常量】
<pre>
例：select name, '唐山' as 地址 from Student
说明：查询表a，显示name列，并添加地址列，其列值都为'唐山'
</pre>
4.1.6【查询返回限制行数(关键字：top percent)】
<pre>
例１：select top 6 name from a
说明：查询表a，显示列name的前６行，top为关键字
例２：select top 60 percent name from a
说明：查询表a，显示列name的60%，percent为关键字
</pre>
4.1.7【查询排序（关键字：order by , asc , desc）】
<pre>
例：
select name
from a
where chengji>=60
order by desc
说明：查询a表中chengji大于等于60的所有行，并按降序显示name列；默认为ＡＳＣ升序
</pre>

4.2``模糊查询  
4.2.1【使用like进行模糊查询】
<pre>
注意：like运算符只用于字符串，所以仅与char和varchar数据类型联合使用
例：select * from a where name like '赵%'
说明：查询显示表a中，name字段第一个字为赵的记录
</pre>
4.2.2【使用between在某个范围内进行查询】
<pre>
例：select * from a where nianling between 18 and 20
说明：查询显示表a中nianling在18到20之间的记录
</pre>
4.2.3【使用in在列举值内进行查询】
<pre>
例：select name from a where address in ('北京','上海','唐山')
说明：查询表a中address值为北京或者上海或者唐山的记录，显示name字段
</pre>

4.3``分组查询  
4.3.1【使用group by进行分组查询】
<pre>
例：select studentID as 学员编号,AVG(score) as 平均成绩 (注释:这里的score是列名)
from score (注释:这里的score是表名)
group by studentID
说明：在表score中查询，按strdentID字段分组，显示strdentID字段和score字段的平均值；
select语句中只允许被分组的列和为每个分组返回的一个值的表达式，例如用一个列名作为参数的聚合函数
</pre>
4.3.2【使用having子句进行分组筛选】
<pre>
例：select studentID as 学员编号,AVG(score) as 平均成绩 (注释:这里的score是列名)
from score (注释:这里的score是表名)
group by studentID
having count(score)>1
说明：接上面例子，显示分组后count(score)>1的行，由于where只能在没有分组时使用，分组后只能使用having来限制条件。
</pre>

4.4``.多表联接查询  
4.4.1内联接  
4.4.1.1【在where子句中指定联接条件】
<pre>
例：select a.name,b.chengji
from a,b
where a.name=b.name
说明：查询表a和表b中name字段相等的记录，并显示表a中的name字段和表b中的chengji字段
</pre>
4.4.1.2【在from子句中使用join…on】
<pre>
例：select a.name,b.chengji
from a inner join b
on (a.name=b.name)
说明：同上
</pre>
4.4.2外联接  
4.4.2.1【左外联接查询】
<pre>
例：select s.name,c.courseID,c.score
from strdents as s
left outer join score as c
on s.scode=c.strdentID
说明：在strdents表和score表中查询满足on条件的行，条件为score表的strdentID与strdents表中的sconde相同
</pre>
4.4.2.2【右外联接查询】
<pre>
例：select s.name,c.courseID,c.score
from strdents as s
right outer join score as c
on s.scode=c.strdentID
说明：在strdents表和score表中查询满足on条件的行，条件为strdents表中的sconde与score表的strdentID相同
</pre>