%%[[_Lab Files]]%%
%%#lab/dbms%%

Customer - c_id, c_name, Mobile, Address, Country

## Group by clause
```plain
select count(c_id), country from customer
groupby country;
```

**output**
| c_id | country |
| ---- | ------- |
| 2    | india   |
| 5    | usa     |
| 3    | uk      | 

put `order by c_id desc` for decreasing order (consmetic changes, doesn't really matter)

## Having clause
```plain
select count(c_id), country from customer
groupby country
having count(c_id) > 10;
```
this gives counts of c_id as per country where count is greater than 10

## join
show emp data, who have dept name = 'CSE'
```plain
select emp.ename, dept.dname from empl, dept
where emp.eno = dept.eno
```

