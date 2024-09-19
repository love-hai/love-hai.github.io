## mysql表结构修改

+ 取消主键

```sql
alter table tableName drop primary key;
```

- 删除表的列

```sql
alter table tableName drop column columnName;
```

+ 设置默认值
  alter table tableName alter column columnName set default value;

## mysql 表数据操作

### 批量更新

#### in

update tableName set columnName = value where columnName in (value1, value2, value3);
有局限性，限制了更新的属性值必须一致。如果不一致，需要分开写多个update语句。

#### insert into... on duplicate key update

insert into tableName (columnName1, columnName2) values (value1, value2) **on duplicate key** update columnName1 = value1, columnName2 = value2;
根据 唯一索引或者primary key 来进行更新，如果存在则更新，不存在则插入。

#### replace into tableName (columnName1, columnName2) values (value1, value2);

如果value的字段不全，会将缺失的字段置为默认值。
究其原因，replace into 操作的本质是对重复的记录先 delete 后 insert，所以如果更新的字段不全会将缺失的字段置为默认值；而 insert into 只是update重复记录，不会改变其它字段。

#### set...case...when...where


```sql
<!-- 代码段 -->
-- 没有where条件，会更新所有的记录,可以使用default()函数来设置默认值
update tb_user
set password = case
    when user_name = 'xxx' then 'xxxpassword'
    when user_name = 'hhh' then 'hhhpassword'
    else default(password)
    end,
    age = case
    when user_name = 'xxx' then 18
    when user_name = 'hhh' then 20
    else default(age)
    end
```

```sql
-- 有where条件，只更新符合条件的记录
update tb_user
set password = case
    when user_name = 'xxx' then 'xxxpassword'
    when user_name = 'hhh' then 'hhhpassword'
    else default(password)
    end,
    age = case
    when user_name = 'xxx' then 18
    when user_name = 'hhh' then 20
    else default(age)
    end
where user_name in ('xxx', 'hhh')
```
