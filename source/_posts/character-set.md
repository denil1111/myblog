title: MY-SQL配置默认字符集on MAC（解决插入中文失败的问题）

date: 2014-04-16 09:03:40

tags: [mysql, 中文, mac]

categories:
- Mysql

---

1. 打开mysql根目录下的my.cnf
2. 在[mysqld]下添加 character-set-server = utf8 
3. 在[client]下添加 default-character-set=utf8
4. 重启mysql
5. 插入中文试试看吧！
