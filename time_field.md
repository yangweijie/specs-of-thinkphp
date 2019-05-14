# 时间相关字段

mysql 里有3中数据存储方式：
int  时间戳
datetime 日期
timestamp 时间戳

建议用datetime 且 默认值为0  '0000-00-00 00:00:00'

但是 tp5 和 tp5.1 里查询的0 表现方式不同

5.0
```
where('create_time', 0)    => create_time = '0' 这个在数据库是查不出 create_time = '0000-00-00 00:00:00'的数据的
whereTime('create_time', 0) => create_time > 1970-01-01 08:00:00
where('create_time = 0')   => (create_time = 0)
where('create_time', Db::raw(0))  create_time = 0

```

5.1
```
where('create_time', 0)    => create_time = 0
whereTime('create_time', 0) => create_time >= 0
where('create_time = 0')   => create_time = 0
where('create_time', Db::raw(0))  create_time = 0
```
所以在使用datetime 默认值为0 的时候 尽量 用 字符串查询或者 Db:raw的方式来保证查询结果为正确未设置过时间的数据

# 参考文档

[MySQL 中的日期时间类型](http://www.cnblogs.com/Wayou/p/mysql_data_type_datetime.html?utm_source=tuicool&utm_medium=referral)
