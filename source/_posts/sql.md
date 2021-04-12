---
title: sql
date: 2020-8-12 13:52:06
tags:
---


## 1、
   <!-- more --> 

 新创建一个专业表t_class，字段如下：
 

mid tinyint--专业号，主键

系部 char（10）--系部名

major  char（10）--专业

***

```


create table t_class(    

mid tinyint,    --专业号，主键

系部 char（10）, --系部名

major char（10） --专业

);


```



## 2、

 给表t_class添加以下数据：

专业号：1，系部：计算机系，专业：物联网

专业号：2，系部：计算机系，专业：软件

专业号：3，系部：计算机系，专业：计算机应用

***

```
insert into user('mid','系部','major')

values

('1','计算机系','物联网'),

('2','计算机系','软件'),

('3','计算机系','计算机应用');
```



## 3、



查询显示学生个人信息：学号、姓名、性别、年龄、专业。

***

```
select   

students.id 学号,students.name 姓名, students.sex 性别, t_class.major 专业，year（now()）- year(bofd) 年龄

from  students,t_class

where students.mid = t_class.mid
```



***

## 4、

查询物联网专业所有同学MySQL数据库课程成绩，并按照成绩从高到底排序，按照成绩查询结果要求显示：学号、姓名、性别、课程名、成绩。

***



```
select  students.id 学号,students.name 姓名, students.sex 性别, courses.cname 课程名称, scores.score 分数

from students,scores, courses,t_class

where students.id = scores.id  and scores.cid = courses.cid and courses.cid = 3
and t_class.mid = 1

ordre by  scores.score  DESC
```



## 5、

统计各课程的平均成绩、最高分及最低分。

***

```
SELECT scores,cid 课程编号,courses.cname 课程名称,AVG(score) 平均分,MAX(score) 最高分, MIN(score) 最低分 
from scores，coureses
where socres.cid = courses.cid 
GROUP BY cid


```

## 6、

统计各科成绩不及格人数。

***

INSERT INTO scores
VALUES
('1','2','2','76.0'),
('1','2','2','60.0'),
('2','1','3','65.0'),
('1','2','3','66.0'),
('1','4','1',NULL),
('1','4','2','81.0'),
('1','4','4','70.0'),
('1','4','6','67.0'),
('1','1','2','50.0'),
('6','2','2','87.0'),
('6','2','3','86.0');

***

```
SELECT cid,COUNT(if( score < 60 , TRUE, null ) )
from scores
GROUP BY cid 
ORDER BY cid 
```

```
SELECT score.cid 课程编号,courses.name 课程名称 ,COUNT(if( scores.score < 60 , TRUE, null ) ) 人数
from scores,courses
WHERE score.cid = courses.cid 
GROUP BY cid 
order by cid DESC
```



# 新建

create database 数据库名

create table 数据表名

alter table 表名 

add 列名 类型 

***



```
create table user
(
	name char(4),
	tel int,
	content int,
	date VARCHAR(20)
)ENGINE=MyISAM DEFAULT CHARSET=gb2312;
```



## 删除表

drop table 表名

## 主键

 字段名 数据类型 primary key ;

## 删除数据

delete 

from 表名

where 

不加条件就代表全删除 ，

## 插入数据

inster  into 表名

values 

(



)

***



```
insert into user(uid,sname,email,tnum,score)
values

('123456','qert','123123@qq.com','1456789','100'),

('123456','qert','123123@qq.com','1456789','100'),

('123456','qert','123123@qq.com','1456789','100');
```

## 修改数据

update 表名

set 列名 =‘要修改的数据’

where 条件

***



```
update 表名
set orededate = '2016-10-01' 要改的数据 
where bid='3'and uid='1003' 条件
条件要放后面
```

## 基础查询

```
select 列名         

form 表名

where 条件
```

distinct 清除重复行

where user in null      --user 为空的

and 并且

or或者

not取反 就是不等于

%任意长度的字符串

_任意单个字符

```
SELECT bname , price
    FROM book
    order by price DESC
    limit 0,3;
    从0取到第三列
```



## 高级查询

 count（*）返回满足条件的行数

*号就是返回所有的行数

```
SELECT cid,COUNT(if( score < 60 , TRUE, null ) ) 返回score中小于60的行数
from scores
GROUP BY cid 
ORDER BY cid 
```

