# 表连接
    表连接：用来同时显示多个表的字段，比如说在员工表中的部门是用代号表示的，然后有个部门表里面有
    部门代号和部门名称的映射关系。然后你同时显示员工名称和部门名称，而同一个表中又不能同时拥有两列。
    所以这个时候我们就需要把这个两个表连接起来，进行查询显示。
    
### 内连接和外连接主要区别
    内连接和外连接的区别是：内连接仅选出两张张表中互相匹配的数据，，既满足后面的的where条件的数据。
    而外连接会选出其他不匹配的记录，即即使不满足后面的条件也可以显示记录
    
#####内连接 和外连接

```sql
-- 内连接
select name,deptname from employee,dept where  deptname.deprno = dept.deprno

-- 外连接以左连接为例

select name,deptname from employee left jion dept on employee.deptno=dept.deptno;
```
    
