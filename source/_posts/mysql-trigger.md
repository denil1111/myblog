title: Trigger in mysql
date: 2014-03-25 11:50:20
tags:
---
##老师sqlserver的例子
	create trigger st1 on borrow
	after insert 
	as
	Begin
	    Declare @num int
	    Declare @cno char(10)
	    select @cno = cno from inserted
	    select @num=count(*) from borrow where cno=@cno
	    If(@num>2)
	    begin
	      Print('一位同学一个学期不可以借三本书！')
	      Rollback
	    End
	End 


##创建
create trigger < trigger name > < when > < action >
on < table name >
for each row
不同于之前的例子
##与sqlserver的区别
1. 首先mysql中不推荐使用@<name>的临时变量，而且@<name>的变量不需要declare申明
2. 变量赋值使用set < name >＝... 的形式,select < name >=< name2 >的形式不会赋值
3. 要使用declare 变量，DELIMITER |   |DELIMITER ;把这个trigger包在里面
4. 如果要在select里赋值，需要用into，且必须用into，因为mysql不能在trigger里输出select
5. mysql中不能使用print
6. mysql中用trigger阻止insert一般使用让程序出错的方式，比如对一个不存在的表操作
