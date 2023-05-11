## SQL的分类



### DDL 数据定义语言

CREATE    \       ALTER     \     DROP    \     RENAME     \     TRUNCATE

### DML 数据库操作语言

INSERT  \   DELETE\  UPDATE   \ SELECT



### DCL sh数据控制语言

COMMIT \ROLLBACK\ SAVEPOINT \ GRANT \ REVOKE



SQL 在winds下不区分大小写 

在Linux要区分大小写



#### 选出所有列

```sql
select * from countries

```





### 别名 AS （alias）

###### 可以用空格代替       别名一般用双引号引上.不要使用单引号' '

+ 没有使用别名

```sql
select employee_id,last_name,department_id from employees
```

![image-20221222144802822](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20221222144802822.png)

+ 加入别名

+ ```sql
  select employee_id as emp_id,last_name as lname,department_id as id from employees
  ```

+ <img src="C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20221222144920067.png" alt="image-20221222144920067" style="zoom:150%;" />





### 去除重复行  distinct

```sql
SELECT DISTINCT department_id FROM employees

```





### 空值参与运算  null

null不等同于0，‘ ’  ，‘null’

参与运算 还是null





### 着重号   ``

将关键字 引出来  就可以将特殊单词当字段名





### 查询常

```sql
SELECT 'Yn' ,111,employee_id,last_name FROM employees
```

![image-20221222151146224](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20221222151146224.png)





### 显示表结构  describe 可以简写 desc

```sql
DESCRIBE employees;
```

![image-20221222151403283](C:\Users\yn\AppData\Roaming\Typora\typora-user-images\image-20221222151403283.png)





#### 过滤 where

限制条件一样

```sql
select * from employees where department_id=90
```

