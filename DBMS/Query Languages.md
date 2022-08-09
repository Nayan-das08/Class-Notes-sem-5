Aug 3, 2022
Chapter - [[DBMS]]
Topics -  

# Query Langs
lang in which user requests info from database

## Categories
* Procedural
* Non procedural

## pure langs
* ### relational algebra
	* **six fundamental operators** - we can write any query with these
		* select 
		* projection
		* union
		* cartesian
		* set difference
		* rename
	* **derived** - used for fast processing
		* division
		* diff types of joins
		* intersection
	
suppose a $Student$ relation is given	
| id  | name   | branch |
| --- | ------ | ------ |
| 1   | nayan  | cse    |
| 2   | adersh | cse    |
| 3   | nayan  | me     | 

## selection
used to select the rows
$\sigma(r)={t | t belongs to r and p(t)}$
where p is a formula in propositional calculus

$\sigma_{branch='cs'}(Student)$ gives the rows where branch = 'cs'
$\sigma_{name='nayan'}(Student)$ gives rows where the name is 'nayan'

## projection
used to select the columns
$\Pi_{name}(Student)$ gives all the name
$\Pi_{name}(Student) \sigma_{branch='cs'}(Student)$ gives all the name where the branch is 'cs'

## union
$r U s={t | t belongs to r or s}$
combines all

## set diff
removes elements of s from r
$r-s$

## cartesian product
multiplies each row of r with each row of s
$r x s$

## rename
rename the table

branch (b_name, b_city, assets)
account (acc_no, b_name, balance)
depositor (c_name, acc_no)
customer (c_name, c_street, c_city)
loan (l_no, b_name, amount)
borrower (c_name, l_no)

### queries
1. find the details of accounts having balance greater than 10000
$\sigma_{balance}(account)$ 

2. find details of customers who live in delhi
$\sigma_{c-city='delhi'}(Customer)$

3. find details of loans having amt less than 5000 and from branch name = 'delhi'
$\sigma_{amount<5000 and b-name='delhi'}$

4. find details of branch situated in delhi and assets > 10,00,000
$\sigma_{b-name='delhi' and asset > 1000000}$
2




