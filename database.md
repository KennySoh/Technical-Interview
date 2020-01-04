# Introduction to Databases - Stanford
https://www.youtube.com/watch?v=spQ7IFksP9g&list=PLroEs25KGvwzmvIxYHRhoGTz9w8LeXek0&index=2 . 
  
Database = set of named **relations** (or **tables**) . 
Each relation has a set of named **attributes**(or **columns**) . 
Each **tuple** (or **row**) has a value for each attribute . 
  
Schmea - Strucutal description of relations in database . 
Instance - the content of database . 
  
NULL - special value for "unkown" or "undefined" . 
Key - attribute whose value is unique in each tuple. Or set of attribute whose combined values are unique . 
  
## Querying relational databases
***
1. Design schema; create using DDL
2. "Bulk load" initial data
3. Repeat: execute queries and modifications
***
  
Ad-hoc queries in high-level language  
***
- All students with GPA> 3.7 applying to Stanford and MIT only
- All engineering departments in CA with <500 applicants
- College with highest average accept rate over last 5 years
***
  
Queries return relations("compositional" , "closed") . 
- "closed" means it returns the same type after query.... returns query . 
- "compositional", Q2 the ability to run query over the result of the previous query.  
***
- Relational Algebra -Formal . 
- SQL - actual/implemented
***

## XML
***
Basic Constructs
- Tagged elements (nested)
- Attributes
- Text
***
```
<Bookstore>
  <Book ISBN="ISBN-0-13-142132 Price="85" Edition = "3rd">
  </Book>
</Bookstore>
```
## JSON
## Relational-Algebra-1