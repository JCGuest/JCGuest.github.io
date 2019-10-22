---
layout: post
title:      "Ruby Episode II: The SQL"
date:       2019-10-21 18:17:14 -0400
permalink:  ruby_episode_ii_the_sql
---

At first glance, SQL can appear to be a little unwieldy and unfriendly. That was my first reaction anyway. SQL (Structured Query Language) is a query language that is used to manage databases and perform various operations on the data in them. The language was developed at IBM by Donald D. Chamberlin and Raymond F. Boyce in the early 1970s. Edgar Codd invented the concept of the relational database and came up with the idea ofstoring data in tables, indexed by primary key and relating by foreign keys to 'normalize' the data. The goal of data normalization is to reduce redundancy. SQL does this beautifully.

I think it is the stripped nature of the language that causes it to appear archaic or oversimplified which may have been what led to my previously mentioned first reaction to it. It also felt like no matter how many readings, code-along's or video tutorials I did; I was not really getting comfortable or fully understanding SQL. It wasn't until I began to write my own queries that I started to see that perhaps the reason it seemed unfriendly and archaic is that SQL is just so simplified and clean that it lacks some of the flashy and refined feeling that other languages have. If something is simple that doesn't have to mean that it is lacking. The fact that SQL has been around since the 70's speaks to its value and efficacy. The most complicated part of SQL for me thus far in my experience with it, "JOIN", is really not that complicated at all. 

JOIN is used to combine multiple tables of data in a database. 

There are several types of joins: 
* Inner Join
* Left Join
* Right Join
* Full Join

Left, right and full joins are known as outer joins.
Here are some visuals to explain the differencs between them: 







![](https://images.squarespace-cdn.com/content/v1/5732253c8a65e244fd589e4c/1464122775537-YVL7LO1L7DU54X1MC2CI/ke17ZwdGBToddI8pDm48kMjn7pTzw5xRQ4HUMBCurC5Zw-zPPgdn4jUwVcJE1ZvWMv8jMPmozsPbkt2JQVr8L3VwxMIOEK7mu3DMnwqv-Nsp2ryTI0HqTOaaUohrI8PIvqemgO4J3VrkuBnQHKRCXIkZ0MkTG3f7luW22zTUABU/image-asset.png?format=300w)
![](http://images.squarespace-cdn.com/content/v1/5732253c8a65e244fd589e4c/1464122797709-C2CDMVSK7P4V0FNNX60B/ke17ZwdGBToddI8pDm48kMjn7pTzw5xRQ4HUMBCurC5Zw-zPPgdn4jUwVcJE1ZvWEV3Z0iVQKU6nVSfbxuXl2c1HrCktJw7NiLqI-m1RSK4p2ryTI0HqTOaaUohrI8PIO5TUUNB3eG_Kh3ocGD53-KZS67ndDu8zKC7HnauYqqk/image-asset.png?format=300w)![](https://images.squarespace-cdn.com/content/v1/5732253c8a65e244fd589e4c/1464122744888-MVIUN2P80PG0YE6H12WY/ke17ZwdGBToddI8pDm48kMjn7pTzw5xRQ4HUMBCurC5Zw-zPPgdn4jUwVcJE1ZvWlExFaJyQKE1IyFzXDMUmzc1HrCktJw7NiLqI-m1RSK4p2ryTI0HqTOaaUohrI8PI-FpwTc-ucFcXUDX7aq6Z4KQhQTkyXNMGg1Q_B1dqyTU/image-asset.png?format=300w)![](https://images.squarespace-cdn.com/content/v1/5732253c8a65e244fd589e4c/1464122981217-RIYH5VL2MF1XWTU2DKVQ/ke17ZwdGBToddI8pDm48kMjn7pTzw5xRQ4HUMBCurC5Zw-zPPgdn4jUwVcJE1ZvWEV3Z0iVQKU6nVSfbxuXl2c1HrCktJw7NiLqI-m1RSK4p2ryTI0HqTOaaUohrI8PIO5TUUNB3eG_Kh3ocGD53-KZS67ndDu8zKC7HnauYqqk/image-asset.png?format=300w )


A join statement might look something like this:   
``` SELECT column_name(s)
FROM first_table
JOIN second_table
ON first_table.column_name = second_table.column_name;```

Queries like the above allow us to tie data together to be able to ask and answer more challenging questions. This join query demonstrates that the syntax is very simple yet the capabilities that arise from its use are profound. Being able to cross-reference and combine data tables was at the heart of the motivation behind the creation of SQL. 

Let's look at some examples that demonstrate the differnces between the types of joins:

Imagine we have the following tables.

```
TEACHERS TABLE             STUDENTS TABLE
id                 student_id   teacher_id
---------------            ------------------------
1                          1            NULL
2                          2            1
3                          3            NULL
```

An inner join returns only the rows of the joined tables that match the query.
(the  ```*```  indicates all columns in a given table)

```
SELECT *
FROM Teachers
JOIN Students
ON Teachers.id = Students.teacher_id;
```
This will return the teacher that has an id that matches any student teacher_id:

```
id  |  student_id |  teacher_id
--------------------------
1           |  2  |  1
```

Now let's take a look at an outer join. Left outer join is the most common one:

```
SELECT
  Teachers.id as teacher_id,
  Students.id as student_id
FROM Teachers
LEFT JOIN Students
ON Teachers.id = Students.teacher_id;
```
This returns every row of the teachers table even if the corresponding "student_id" column for that teahcer is empty:

```
teacher_id  |  student_id
--------------------------
1           |  2
2           |  NULL
3           |  NULL
```

Another feature that you may notice being used in this query is the "AS" statement. This works by essentially assigning the column to a variable to make the output cleaner and easier to read as well as allowing this new column name to be used in more complex functions.

A right join is essentially the same as a left join except it returns all the rows from the right-most colomn:

```
SELECT
  Teachers.id as teacher_id,
  Students.id as student_id
FROM Teachers
RIGHT OUTER JOIN Students
ON Teachers.id = Students.teacher_id;
```

```
teacher_id     |  student_id
--------------------------
NULL           |  1
1              |  2
NULL           |  3
```

And as you migh have guessed by now; the full join returns all rows from all tables:

```
SELECT
  Teachers.id as teacher_id,
  Students.id as student_id
FROM Teachers
FULL OUTER JOIN Students
ON Teachers.id = Students.teacher_id;
```

```
teacher_id     |  student_id
--------------------------
NULL           |  1
1              |  2
NULL           |  3
2              |  NULL
3              |  NULL
```

Understanding how these functions work and how to use them is a major portion of understanding the entire language itself. I have come to love SQL and I look forward to gaining more understanding as I come to understand why it is one of the oldest and most commonly used language there are.
