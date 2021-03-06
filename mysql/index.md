## 索引管理

添加索引

```sql
alter table student add index name (`name`);
```

添加唯一索引

```sql
alter table student add unique index uid (`uid`);
```

添加联合索引

```sql
alter table student add index idx1 (`gid`, `group_id`, `area_id`);
```

添加前缀索引

```sql
alter table student add index ooid (`ooid(50)`);
```

同时添加多个索引

```sql
alter table student add unique index uid (`uid`), add index name (`name`), add index age (`age`);
```

删除索引

```sql
alter table student drop index uid;
```

同时删除多个索引

```sql
alter table student drop index name, drop index age;
```

查看索引

```sql
show create table student\G
```

查看索引（方法2）

```sql
show index from student
```

- [13.1.8 ALTER TABLE Syntax](https://dev.mysql.com/doc/refman/5.7/en/alter-table.html)

给值有重复的列添加唯一索引会报错，可以使用以下方法找出重复的行。

```sql
select unique_id,count(unique_id)
from yourtblname
group by unique_id
having count(unique_id) >1;
```

- [#1062 - Duplicate entry '' for key 'unique_id' When Trying to add UNIQUE KEY (MySQL)](https://stackoverflow.com/questions/17823322/1062-duplicate-entry-for-key-unique-id-when-trying-to-add-unique-key-my)

使用 `IGNORE` 参数可以实现在添加唯一索引的同时将重复的记录删除只保留一条。

```sql
alter ignore table mytable add unique index myindex (a, b, c, d);
```

但是，这种方式只在 MySQL 5.7.4 之前的版本有效。

- [Removing duplicates with unique index](https://dev.mysql.com/doc/refman/5.7/en/alter-table.html)

## 使用索引

强制走索引
