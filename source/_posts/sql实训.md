---
title: sql实训
date: 2021-01-14 12:13:35
tags:
---
哎 做完了

```


--新建数据库

create database software087;

--新建数据表

use software090;
```

 <!-- more -->

```
create table student
	(
		stuID char(10) not null primary key,
		stuName char(8),
		stuSex char(2) default'男',
		Birthday date
		);

create table course
	(
		courseID char(3) not null primary key,
		courseName varchar(20) not null
		);

create table sc
	(
		stuID char(10) not null,
		courseID char(3) not null,
		Grade decimal(4,1),
		primary key(stuID,courseID),
		CONSTRAINT fk_sc_stuID foreign key(stuID) references student(stuID),
		CONSTRAINT fk_sc_courseID foreign key(courseID) references course(courseID)
		);

create table teacher
	(
		teacherID char(3) not null primary key,
		teacherName char(8) not null,
		teacherSex char(2)
		);

create table teachering
	(
		teacherID char(3) not null,
		courseID char(3) not null,
		primary key(teacherID,courseID),
		CONSTRAINT fk_teachering_teacherID foreign key(teacherID) references teacher(teacherID),
		CONSTRAINT fk_teachering_courseID foreign key(courseID) references course(courseID)
		);

insert into student
	values( '2014030701','张三','男','1987-01-12'),
	      ( '2014020701','王宁','男','1988-03-20'),
	      ( '2014030702','王芳','女','1987-11-15'),
	      ( '2014020704','李立','男','1986-12-30'),
	      ( '2014030703','田甜','女','1987-09-10');

insert into course
	values('C01','大学英语'),
	      ('C02','数据库原理及应用'),
	      ('C03','操作系统');

insert into sc
	values('2014030701','C02','98'),
	      ('2014030701','C03','86'),
	      ('2014030703','C01','79'),
	      ('2014030703','C02','94'),
	      ('2014030703','C03','55');

insert into teacher
	values('t01','李勇','男'),
	      ('t02','钱军','男'),
	      ('t03','王旺','男'),
	      ('t04','张成','男'),
	      ('t05','李丽','女');

insert into teachering
	values('t01','C01'),
	      ('t02','C02'),
	      ('t04','C03');

1
select stuID as 学号，stuName as 姓名,Birthday as 出生日期
from student
where stuName like '王%' and 男的 懒得写了;

2
select *
from sc
limit 3;

3
SELECT  course.courseID 课程号, courseName 课程号, COUNT(*)人数, MAX(Grade) 最高分
FROM sc,course
WHERE SC.courseID = course.courseID 
GROUP BY courseName

4
select student .stuName, student.stuID
from sc as a join student as b on a.stuID = b.stuID
join student on student.stuID = A.stuID

视图

CREATE VIEW stu_sc_teacher

SELECT  student.stuID 学号, student.stuName 姓名 ,sc.courseID 课程号,course.courseName 课程名 ,sc.Grade 成绩 , teachering.teacherID 教师编号 , teacher.teacherName 教师名称
FROM student,sc,course,teachering,teacher
WHERE student.stuID = sc.stuID and sc.courseID = course.courseID and sc.courseID = teachering.courseID and teachering.teacherID = teacher.teacherID
ORDER BY student.stuID 


SELECT  student.stuName,student.stuID,sc.courseID,course.courseName,sc.Grade, teachering.teacherID
FROM student,sc,course,teachering
WHERE student.stuID = sc.stuID and 
sc.courseID = course.courseID and 
sc.courseID = teachering.courseID and
ORDER BY student.stuID 


存储1
delimiter //
CREATE PROCEDURE proc_1()
BEGIN
SELECT student.stuID 学号, student.stuName 姓名 ,student.stuSex 性别,course.courseID 课程号,course.courseName 课程名,sc.Grade 成绩
FROM student,course,sc
WHERE student.stuID = sc.stuID and course.courseID = sc.courseID and sc.Grade < 60
ORDER BY student.stuID;
END;//
delimiter;


delimiter //
CREATE PROCEDURE proc_1()
BEGIN
SELECT student.stuID , student.stuName ,student.stuSex ,course.courseID,course.courseName,sc.Grade
FROM student,course,sc
WHERE student.stuID = sc.stuID and course.courseID = sc.courseID and sc.Grade < 60
ORDER BY student.stuID;
END;//
delimiter;

存储2
delimiter //
CREATE PROCEDURE proc_2(in xh char(10))
BEGIN
SELECT  *
FROM student
WHERE stuID = xh;
END;//
delimiter;

存储3

delimiter //
CREATE PROCEDURE proc_3(in cid_tmp char(3) , OUT sum_grade decimal(4,1))
BEGIN
SELECT  SUM(Grade) INTO sum_grade
FROM sc
WHERE courseID = cid_tmp;
END;//
delimiter;


set @grade=0;
call proc_3('C03',@grade);
SELECT @grade 成绩







delimiter //
CREATE TRIGGER student_sno
AFTER UPDATE 
ON student
FOR EACH ROW
BEGIN
if (
select stuID
from sc
where old.stuID != new.stuID
) is NULL THEN
UPDATE sc
SET stuID = new.stuID
WHERE stuID = old.stuID;
END;//
delimiter;


```

