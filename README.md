# [Your Name]
# [Your Student ID]
# [Course Name/Number]
# [Professor's Name]
# [Date]

**Subject: Documentation for Extracted SQL Queries from Korth Textbook (Chapters 3 & 4)**

## 1. Introduction

This document provides documentation for the specific SQL `SELECT` queries extracted from Chapters 3 and 4 of the provided textbook PDF ("korth-66-182.pdf"). The queries included focus on intermediate and advanced SQL concepts such as joins (including outer joins), aggregate functions with grouping/having, subqueries (nested, correlated, scalar), set operations, pattern matching, ordering, and `WITH` clauses. Basic `SELECT` statements (e.g., simple projections or selections on a single table with simple conditions) have been excluded as per the requirement.

Each query listed below is accompanied by:
* A description of its purpose (what question it answers).
* Notes on the specific SQL techniques demonstrated.
* A reference to its context in the textbook PDF.
* A placeholder for the query's output screenshot.

The corresponding `.sql` file containing all these queries is submitted alongside this document.

## 2. Extracted SQL Queries and Explanations

**--- Chapter 3 Queries ---**

### Query 1: Arithmetic Expression in SELECT

* **Purpose:** To retrieve instructor details, showing a potential 10% salary increase by multiplying the `salary` attribute by 1.1.
* **Technique(s):** Arithmetic expression (`*`) within the `SELECT` clause.
* **Source Context:** Chapter 3, Section 3.3.1.
* **SQL Query:**
    ```sql
    SELECT ID, name, dept_name, salary * 1.1
    FROM instructor;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 2: WHERE clause with multiple conditions (AND)

* **Purpose:** To find the names of instructors in the Computer Science department with a salary greater than $70,000.
* **Technique(s):** `WHERE` clause with multiple conditions combined using the logical `AND` operator. Comparison operators (`=`, `>`).
* **Source Context:** Chapter 3, Section 3.3.1.
* **SQL Query:**
    ```sql
    SELECT name
    FROM instructor
    WHERE dept_name = 'Comp. Sci.' AND salary > 70000;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 3: Join using WHERE Clause (Implicit Join)

* **Purpose:** To retrieve the names of instructors along with their department names and the building name of their department by combining information from the `instructor` and `department` tables.
* **Technique(s):** Implicit join using a Cartesian product in the `FROM` clause filtered by an equality condition in the `WHERE` clause. Attribute disambiguation using `relation.attribute` notation (e.g., `instructor.dept_name`).
* **Source Context:** Chapter 3, Section 3.3.2.
* **SQL Query:**
    ```sql
    SELECT name, instructor.dept_name, building
    FROM instructor, department
    WHERE instructor.dept_name = department.dept_name;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 4: Join using WHERE Clause (Implicit Join)

* **Purpose:** To retrieve instructor names and the course identifiers for courses they have taught by matching `instructor` and `teaches` relations on the `ID` attribute.
* **Technique(s):** Implicit join via `WHERE` clause condition (`instructor.ID = teaches.ID`).
* **Source Context:** Chapter 3, Section 3.3.2.
* **SQL Query:**
    ```sql
    SELECT name, course_id
    FROM instructor, teaches
    WHERE instructor.ID = teaches.ID;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 5: Join using WHERE Clause with Additional Condition

* **Purpose:** To find instructor names and course identifiers specifically for instructors in the Computer Science department who have taught a course.
* **Technique(s):** Implicit join via `WHERE` clause with multiple conditions (`instructor.ID = teaches.ID` and `instructor.dept_name = 'Comp. Sci.'`).
* **Source Context:** Chapter 3, Section 3.3.2.
* **SQL Query:**
    ```sql
    SELECT name, course_id
    FROM instructor, teaches
    WHERE instructor.ID = teaches.ID AND instructor.dept_name = 'Comp. Sci.';
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 6: Natural Join

* **Purpose:** To find the names of instructors and the course IDs of all courses they taught, combining `instructor` and `teaches` based on common attributes (implicitly `ID`).
* **Technique(s):** `NATURAL JOIN` operation. Automatically joins on attributes with the same name (`ID`) and includes the common attribute only once in the result.
* **Source Context:** Chapter 3, Section 3.3.3.
* **SQL Query:**
    ```sql
    SELECT name, course_id
    FROM instructor NATURAL JOIN teaches;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 7: Natural join and Cartesian product with WHERE clause

* **Purpose:** To list the names of instructors along with the titles of the courses they teach. It first joins `instructor` and `teaches` naturally, then combines this result with `course` based on matching `course_id` via the `WHERE` clause.
* **Technique(s):** Combination of `NATURAL JOIN` and implicit join (Cartesian product filtered by `WHERE`). Attribute disambiguation (`teaches.course_id`).
* **Source Context:** Chapter 3, Section 3.3.3.
* **SQL Query:**
    ```sql
    SELECT name, title
    FROM instructor NATURAL JOIN teaches, course
    WHERE teaches.course_id = course.course_id;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 8: Multiple Natural Joins (Potentially Incorrect Example)

* **Purpose:** Intended to list instructor names and course titles, but uses consecutive `NATURAL JOIN` operations.
* **Technique(s):** Multiple `NATURAL JOIN` operations. This example highlights a potential pitfall: the second natural join will equate *all* common attributes (both `course_id` and `dept_name`), potentially excluding instructors teaching courses outside their own department.
* **Source Context:** Chapter 3, Section 3.3.3.
* **SQL Query:**
    ```sql
    SELECT name, title
    FROM instructor NATURAL JOIN teaches NATURAL JOIN course;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 9: Join with USING clause

* **Purpose:** To correctly list instructor names and course titles (addressing the issue in Query 8) by explicitly specifying that the join between the `(instructor natural join teaches)` result and `course` should only match on `course_id`.
* **Technique(s):** `JOIN...USING` clause. Specifies the column(s) for joining, avoiding unintended matching on other common columns (like `dept_name`).
* **Source Context:** Chapter 3, Section 3.3.3.
* **SQL Query:**
    ```sql
    SELECT name, title
    FROM (instructor NATURAL JOIN teaches) JOIN course USING (course_id);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 10: Renaming attribute using AS

* **Purpose:** To retrieve instructor names and course IDs, renaming the `name` attribute in the result to `instructor_name`.
* **Technique(s):** `AS` clause in the `SELECT` list to rename an output attribute.
* **Source Context:** Chapter 3, Section 3.4.1.
* **SQL Query:**
    ```sql
    SELECT name AS instructor_name, course_id
    FROM instructor, teaches
    WHERE instructor.ID = teaches.ID;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 11: Renaming relations using AS (Aliases)

* **Purpose:** To retrieve instructor names and course IDs, using shortened aliases (`T` for `instructor`, `S` for `teaches`) for brevity and clarity in referencing attributes.
* **Technique(s):** `AS` clause in the `FROM` list to define relation aliases (correlation names/tuple variables). Using aliases to qualify attribute names (e.g., `T.name`, `S.course_id`).
* **Source Context:** Chapter 3, Section 3.4.1.
* **SQL Query:**
    ```sql
    SELECT T.name, S.course_id
    FROM instructor AS T, teaches AS S
    WHERE T.ID = S.ID;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 12: Self-Join

* **Purpose:** To find the names of instructors whose salary is greater than at least one instructor in the Biology department.
* **Technique(s):** Self-join by listing the same relation (`instructor`) twice in the `FROM` clause with different aliases (`T` and `S`) [cite: 521-522, 524]. Allows comparison of values between different tuples of the same relation.
* **Source Context:** Chapter 3, Section 3.4.1.
* **SQL Query:**
    ```sql
    SELECT DISTINCT T.name
    FROM instructor AS T, instructor AS S
    WHERE T.salary > S.salary AND S.dept_name = 'Biology';
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 13: WHERE clause with LIKE for pattern matching

* **Purpose:** To find the names of departments whose building name contains the substring 'Watson'.
* **Technique(s):** `LIKE` operator for pattern matching in strings. Wildcard character `%` matches any substring.
* **Source Context:** Chapter 3, Section 3.4.2.
* **SQL Query:**
    ```sql
    SELECT dept_name
    FROM department
    WHERE building LIKE '%Watson%';
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 14: Selecting all attributes from one table in a join

* **Purpose:** To select all attributes from the `instructor` relation for those instructors who have taught a course (by joining with `teaches`).
* **Technique(s):** Using `relation_name.*` syntax in the `SELECT` clause to retrieve all columns from a specific table involved in a join.
* **Source Context:** Chapter 3, Section 3.4.3.
* **SQL Query:**
    ```sql
    SELECT instructor.*
    FROM instructor, teaches
    WHERE instructor.ID = teaches.ID;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 15: ORDER BY clause

* **Purpose:** To list the names of instructors in the Physics department in alphabetical (ascending) order.
* **Technique(s):** `ORDER BY` clause to sort the result set. Default sort order is ascending (`ASC`).
* **Source Context:** Chapter 3, Section 3.4.4.
* **SQL Query:**
    ```sql
    SELECT name
    FROM instructor
    WHERE dept_name = 'Physics'
    ORDER BY name;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 16: ORDER BY multiple attributes with specified directions

* **Purpose:** To list all instructor details, ordered first by salary in descending order, and then by name in ascending order for instructors with the same salary.
* **Technique(s):** `ORDER BY` clause with multiple attributes. Specifying sort direction using `DESC` (descending) and `ASC` (ascending).
* **Source Context:** Chapter 3, Section 3.4.4.
* **SQL Query:**
    ```sql
    SELECT *
    FROM instructor
    ORDER BY salary DESC, name ASC;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 17: WHERE clause with BETWEEN operator

* **Purpose:** To find the names of instructors whose salary is between $90,000 and $100,000 (inclusive).
* **Technique(s):** `BETWEEN` operator to specify a range in the `WHERE` clause. Equivalent to `>=` and `<=`.
* **Source Context:** Chapter 3, Section 3.4.5.
* **SQL Query:**
    ```sql
    SELECT name
    FROM instructor
    WHERE salary BETWEEN 90000 AND 100000;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 18: Tuple comparison in WHERE clause

* **Purpose:** To find instructor names and course IDs where the instructor ID matches the teaches ID and the department name is 'Biology'. This example uses tuple comparison syntax.
* **Technique(s):** Tuple comparison `(column1, column2) = (value1, value2)` in the `WHERE` clause. (Note: Support for this syntax might vary across SQL implementations [cite: 579 footnote]).
* **Source Context:** Chapter 3, Section 3.4.5.
* **SQL Query:**
    ```sql
    SELECT name, course_id
    FROM instructor, teaches
    WHERE (instructor.ID, dept_name) = (teaches.ID, 'Biology');
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 19: Set Operation: UNION

* **Purpose:** To find the set of all unique course IDs taught either in Fall 2009 or in Spring 2010 (or both).
* **Technique(s):** `UNION` set operator. Combines results of two `SELECT` statements and automatically eliminates duplicate rows.
* **Source Context:** Chapter 3, Section 3.5.1.
* **SQL Query:**
    ```sql
    (SELECT course_id
     FROM section
     WHERE semester = 'Fall' AND year = 2009)
    UNION
    (SELECT course_id
     FROM section
     WHERE semester = 'Spring' AND year = 2010);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 20: Set Operation: UNION ALL

* **Purpose:** To find all course IDs taught in Fall 2009 or Spring 2010, retaining all duplicate occurrences from both semesters.
* **Technique(s):** `UNION ALL` set operator. Combines results but does not eliminate duplicates.
* **Source Context:** Chapter 3, Section 3.5.1.
* **SQL Query:**
    ```sql
    (SELECT course_id
     FROM section
     WHERE semester = 'Fall' AND year = 2009)
    UNION ALL
    (SELECT course_id
     FROM section
     WHERE semester = 'Spring' AND year = 2010);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 21: Set Operation: INTERSECT

* **Purpose:** To find the set of unique course IDs taught in *both* Fall 2009 and Spring 2010.
* **Technique(s):** `INTERSECT` set operator. Returns only rows present in the results of both `SELECT` statements and automatically eliminates duplicates.
* **Source Context:** Chapter 3, Section 3.5.2.
* **SQL Query:**
    ```sql
    (SELECT course_id
     FROM section
     WHERE semester = 'Fall' AND year = 2009)
    INTERSECT
    (SELECT course_id
     FROM section
     WHERE semester = 'Spring' AND year = 2010);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 22: Set Operation: INTERSECT ALL

* **Purpose:** To find course IDs taught in both Fall 2009 and Spring 2010, where the number of times a course ID appears in the result is the minimum of its occurrences in the two input sets.
* **Technique(s):** `INTERSECT ALL` set operator. Retains duplicates based on the minimum frequency in the input results.
* **Source Context:** Chapter 3, Section 3.5.2.
* **SQL Query:**
    ```sql
    (SELECT course_id
     FROM section
     WHERE semester = 'Fall' AND year = 2009)
    INTERSECT ALL
    (SELECT course_id
     FROM section
     WHERE semester = 'Spring' AND year = 2010);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 23: Set Operation: EXCEPT

* **Purpose:** To find the set of unique course IDs taught in Fall 2009 but *not* in Spring 2010.
* **Technique(s):** `EXCEPT` set operator (or `MINUS` in some implementations like Oracle [cite: 609 footnote]). Performs set difference and automatically eliminates duplicates.
* **Source Context:** Chapter 3, Section 3.5.3.
* **SQL Query:**
    ```sql
    (SELECT course_id
     FROM section
     WHERE semester = 'Fall' AND year = 2009)
    EXCEPT
    (SELECT course_id
     FROM section
     WHERE semester = 'Spring' AND year = 2010);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 24: Set Operation: EXCEPT ALL

* **Purpose:** To find course IDs taught in Fall 2009 but not Spring 2010, retaining duplicates from the first set minus duplicates from the second set.
* **Technique(s):** `EXCEPT ALL` set operator. Performs set difference while considering duplicate counts.
* **Source Context:** Chapter 3, Section 3.5.3.
* **SQL Query:**
    ```sql
    (SELECT course_id
     FROM section
     WHERE semester = 'Fall' AND year = 2009)
    EXCEPT ALL
    (SELECT course_id
     FROM section
     WHERE semester = 'Spring' AND year = 2010);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 25: Checking for NULL values

* **Purpose:** To find the names of instructors whose salary value is NULL.
* **Technique(s):** `IS NULL` predicate in the `WHERE` clause to test for null values. Standard equality comparison (`= NULL`) evaluates to `unknown`.
* **Source Context:** Chapter 3, Section 3.6.
* **SQL Query:**
    ```sql
    SELECT name
    FROM instructor
    WHERE salary IS NULL;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 26: Aggregate function AVG

* **Purpose:** To find the average salary of instructors in the Computer Science department.
* **Technique(s):** `AVG()` aggregate function. Applied to the `salary` column for rows matching the `WHERE` clause.
* **Source Context:** Chapter 3, Section 3.7.1.
* **SQL Query:**
    ```sql
    SELECT AVG(salary)
    FROM instructor
    WHERE dept_name = 'Comp. Sci.';
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 27: Aggregate function AVG with Alias

* **Purpose:** To find the average salary of Computer Science instructors, giving the resulting column a meaningful name (`avg_salary`).
* **Technique(s):** `AVG()` aggregate function. `AS` clause used to name the result column of the aggregation.
* **Source Context:** Chapter 3, Section 3.7.1.
* **SQL Query:**
    ```sql
    SELECT AVG(salary) AS avg_salary
    FROM instructor
    WHERE dept_name = 'Comp. Sci.';
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 28: Aggregate function COUNT DISTINCT

* **Purpose:** To find the total number of *distinct* instructors who taught a course in the Spring 2010 semester.
* **Technique(s):** `COUNT(DISTINCT column)` aggregate function. Counts unique values in the specified column (`ID`), ensuring each instructor is counted only once even if they taught multiple sections.
* **Source Context:** Chapter 3, Section 3.7.1.
* **SQL Query:**
    ```sql
    SELECT COUNT(DISTINCT ID)
    FROM teaches
    WHERE semester = 'Spring' AND year = 2010;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 29: Aggregate function COUNT(*)

* **Purpose:** To find the total number of tuples (rows) in the `course` relation.
* **Technique(s):** `COUNT(*)` aggregate function. Counts all rows in the result set defined by the `FROM` and `WHERE` clauses (or the entire table if no `WHERE` clause).
* **Source Context:** Chapter 3, Section 3.7.1.
* **SQL Query:**
    ```sql
    SELECT COUNT(*)
    FROM course;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 30: Aggregate function with GROUP BY

* **Purpose:** To find the average salary for each department.
* **Technique(s):** `GROUP BY` clause. Groups rows based on the values in the specified column (`dept_name`). `AVG()` aggregate function applied to each group independently.
* **Source Context:** Chapter 3, Section 3.7.2.
* **SQL Query:**
    ```sql
    SELECT dept_name, AVG(salary) AS avg_salary
    FROM instructor
    GROUP BY dept_name;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 31: Aggregate function with GROUP BY and JOIN

* **Purpose:** To find the number of distinct instructors in each department who taught a course in Spring 2010.
* **Technique(s):** `NATURAL JOIN` to combine `instructor` and `teaches`. `WHERE` clause to filter for Spring 2010. `GROUP BY dept_name` to group by department. `COUNT(DISTINCT ID)` aggregate function applied per group.
* **Source Context:** Chapter 3, Section 3.7.2.
* **SQL Query:**
    ```sql
    SELECT dept_name, COUNT(DISTINCT ID) AS instr_count
    FROM instructor NATURAL JOIN teaches
    WHERE semester = 'Spring' AND year = 2010
    GROUP BY dept_name;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 32: HAVING clause to filter groups

* **Purpose:** To find the departments where the average instructor salary is more than $42,000.
* **Technique(s):** `GROUP BY` clause to group instructors by department. `HAVING` clause to filter these groups based on a condition involving an aggregate function (`AVG(salary) > 42000`). `HAVING` applies *after* grouping, unlike `WHERE` which applies before.
* **Source Context:** Chapter 3, Section 3.7.3.
* **SQL Query:**
    ```sql
    SELECT dept_name, AVG(salary) AS avg_salary
    FROM instructor
    GROUP BY dept_name
    HAVING AVG(salary) > 42000;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 33: GROUP BY multiple columns with HAVING clause

* **Purpose:** To find the average total credits (`tot_cred`) for students enrolled in each course section offered in 2009, but only for sections that had at least 2 students enrolled.
* **Technique(s):** `NATURAL JOIN` of `takes` and `student`. `WHERE` clause to filter for year 2009. `GROUP BY` multiple columns (`course_id`, `semester`, `year`, `sec_id`) to group by section. `HAVING` clause with `COUNT(ID) >= 2` to filter groups (sections) based on the number of students. `AVG(tot_cred)` calculated per qualifying group.
* **Source Context:** Chapter 3, Section 3.7.3.
* **SQL Query:**
    ```sql
    SELECT course_id, semester, year, sec_id, AVG(tot_cred)
    FROM takes NATURAL JOIN student
    WHERE year = 2009
    GROUP BY course_id, semester, year, sec_id
    HAVING COUNT(ID) >= 2;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 34: Aggregate SUM (handles NULLs)

* **Purpose:** To calculate the total salary expenditure for all instructors.
* **Technique(s):** `SUM()` aggregate function. Ignores NULL values in the input collection by default.
* **Source Context:** Chapter 3, Section 3.7.4.
* **SQL Query:**
    ```sql
    SELECT SUM(salary)
    FROM instructor;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 35: Subquery with IN operator

* **Purpose:** To find all unique course IDs taught in Fall 2009 that were also taught in Spring 2010. Alternative to using `INTERSECT`.
* **Technique(s):** Nested subquery. `IN` operator tests for membership in the set of values returned by the subquery [cite: 721, 725-727].
* **Source Context:** Chapter 3, Section 3.8.1.
* **SQL Query:**
    ```sql
    SELECT DISTINCT course_id
    FROM section
    WHERE semester = 'Fall' AND year = 2009 AND
          course_id IN (SELECT course_id
                          FROM section
                          WHERE semester = 'Spring' AND year = 2010);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 36: Subquery with NOT IN operator

* **Purpose:** To find all unique course IDs taught in Fall 2009 but *not* in Spring 2010. Alternative to using `EXCEPT`.
* **Technique(s):** Nested subquery. `NOT IN` operator tests for absence of membership in the set of values returned by the subquery.
* **Source Context:** Chapter 3, Section 3.8.1.
* **SQL Query:**
    ```sql
    SELECT DISTINCT course_id
    FROM section
    WHERE semester = 'Fall' AND year = 2009 AND
          course_id NOT IN (SELECT course_id
                              FROM section
                              WHERE semester = 'Spring' AND year = 2010);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 37: NOT IN with an enumerated list

* **Purpose:** To select the names of instructors whose names are neither 'Mozart' nor 'Einstein'.
* **Technique(s):** `NOT IN` operator used with an explicitly listed set of values.
* **Source Context:** Chapter 3, Section 3.8.1.
* **SQL Query:**
    ```sql
    SELECT DISTINCT name
    FROM instructor
    WHERE name NOT IN ('Mozart', 'Einstein');
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 38: Subquery with tuple comparison using IN

* **Purpose:** To find the total number of distinct students who have taken any course section taught by the instructor with ID 10101.
* **Technique(s):** Nested subquery returning multiple columns (a relation). `IN` operator used with tuple comparison to check if a tuple from `takes` matches a tuple returned by the subquery. `COUNT(DISTINCT ID)` aggregation.
* **Source Context:** Chapter 3, Section 3.8.1.
* **SQL Query:**
    ```sql
    SELECT COUNT(DISTINCT ID)
    FROM takes
    WHERE (course_id, sec_id, semester, year) IN (SELECT course_id, sec_id, semester, year
                                                   FROM teaches
                                                   WHERE teaches.ID = 10101);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 39: Subquery with > SOME comparison

* **Purpose:** To find the names of instructors whose salary is greater than the salary of *at least one* instructor in the Biology department.
* **Technique(s):** Nested subquery returning a set of salary values. `> SOME` (or `> ANY` [cite: 754 footnote]) comparison operator. Returns true if the comparison is true for at least one value in the subquery result.
* **Source Context:** Chapter 3, Section 3.8.2.
* **SQL Query:**
    ```sql
    SELECT name
    FROM instructor
    WHERE salary > SOME (SELECT salary
                           FROM instructor
                           WHERE dept_name = 'Biology');
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 40: Subquery with > ALL comparison

* **Purpose:** To find the names of instructors whose salary is greater than the salary of *every* instructor in the Biology department.
* **Technique(s):** Nested subquery returning a set of salary values. `> ALL` comparison operator. Returns true if the comparison is true for all values in the subquery result.
* **Source Context:** Chapter 3, Section 3.8.2.
* **SQL Query:**
    ```sql
    SELECT name
    FROM instructor
    WHERE salary > ALL (SELECT salary
                          FROM instructor
                          WHERE dept_name = 'Biology');
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 41: Subquery with >= ALL comparison (finding maximum)

* **Purpose:** To find the department(s) that have the highest average salary.
* **Technique(s):** Nested subquery calculates the average salary for *all* departments. Outer query calculates average salary per department and uses `>= ALL` comparison to find the department(s) whose average salary is greater than or equal to every average salary value returned by the subquery. Involves aggregation (`AVG`) and grouping (`GROUP BY`) in both outer query (`HAVING` clause) and subquery.
* **Source Context:** Chapter 3, Section 3.8.2.
* **SQL Query:**
    ```sql
    SELECT dept_name
    FROM instructor
    GROUP BY dept_name
    HAVING AVG(salary) >= ALL (SELECT AVG(salary)
                                FROM instructor
                                GROUP BY dept_name);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 42: Correlated subquery with EXISTS

* **Purpose:** To find all course IDs taught in both Fall 2009 and Spring 2010. Another alternative to `INTERSECT` or `IN`.
* **Technique(s):** `EXISTS` operator. Tests if the subquery returns any rows (is non-empty). Correlated subquery: the subquery references a table alias (`S`) from the outer query (`S.course_id = T.course_id`). The subquery is evaluated for each row processed by the outer query.
* **Source Context:** Chapter 3, Section 3.8.3.
* **SQL Query:**
    ```sql
    SELECT course_id
    FROM section AS S
    WHERE semester = 'Fall' AND year = 2009 AND
          EXISTS (SELECT *
                  FROM section AS T
                  WHERE semester = 'Spring' AND year = 2010 AND
                        S.course_id = T.course_id);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 43: Correlated subquery with NOT EXISTS and EXCEPT (Set Containment)

* **Purpose:** To find all students who have taken *all* courses offered in the Biology department. This simulates the superset operation ("set of courses taken by student" contains "set of Biology courses").
* **Technique(s):** `NOT EXISTS` operator. Correlated subquery. Uses `EXCEPT` within the subquery to find Biology courses *not* taken by the student. If this set difference is empty (i.e., `NOT EXISTS` is true), the student has taken all Biology courses.
* **Source Context:** Chapter 3, Section 3.8.3.
* **SQL Query:**
    ```sql
    SELECT DISTINCT S.ID, S.name
    FROM student AS S
    WHERE NOT EXISTS ((SELECT course_id
                       FROM course
                       WHERE dept_name = 'Biology')
                      EXCEPT
                      (SELECT T.course_id
                       FROM takes AS T
                       WHERE S.ID = T.ID));
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 44: Subquery with UNIQUE

* **Purpose:** To find all courses that were offered at most once in 2009.
* **Technique(s):** `UNIQUE` predicate. Returns true if the subquery result contains no duplicate tuples. Note: `UNIQUE` handles NULLs differently than equality predicates and is not widely implemented [cite: 774 footnote, 781-782].
* **Source Context:** Chapter 3, Section 3.8.4.
* **SQL Query:**
    ```sql
    SELECT T.course_id
    FROM course AS T
    WHERE UNIQUE (SELECT R.course_id
                    FROM section AS R
                    WHERE T.course_id = R.course_id AND R.year = 2009);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 45: Equivalent query using COUNT instead of UNIQUE

* **Purpose:** To find all courses that were offered at most once in 2009, using `COUNT` instead of the `UNIQUE` predicate.
* **Technique(s):** Correlated subquery using `COUNT` aggregate. Checks if the count of sections for a given course in 2009 is less than or equal to 1.
* **Source Context:** Chapter 3, Section 3.8.4.
* **SQL Query:**
    ```sql
    SELECT T.course_id
    FROM course AS T
    WHERE 1 >= (SELECT count(R.course_id)
                 FROM section AS R
                 WHERE T.course_id= R.course_id AND R.year = 2009);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 46: Subquery with NOT UNIQUE

* **Purpose:** To find all courses that were offered at least twice (i.e., more than once) in 2009.
* **Technique(s):** `NOT UNIQUE` predicate. Returns true if the subquery result contains duplicate tuples.
* **Source Context:** Chapter 3, Section 3.8.4.
* **SQL Query:**
    ```sql
    SELECT T.course_id
    FROM course AS T
    WHERE NOT UNIQUE (SELECT R.course_id
                        FROM section AS R
                        WHERE T.course_id = R.course_id AND R.year = 2009);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 47: Subquery in the FROM clause (Derived Table)

* **Purpose:** To find the average instructors' salaries only for those departments where the average salary is greater than $42,000. Alternative to using `HAVING`.
* **Technique(s):** Subquery used in the `FROM` clause. The result of the subquery (which calculates average salary per department) acts as a temporary table (derived table) that the outer query selects from. The filtering condition (`avg_salary > 42000`) is applied in the outer query's `WHERE` clause.
* **Source Context:** Chapter 3, Section 3.8.5 [cite: 783-788, 790].
* **SQL Query:**
    ```sql
    SELECT dept_name, avg_salary
    FROM (SELECT dept_name, AVG(salary) AS avg_salary
          FROM instructor
          GROUP BY dept_name) AS derived_table_alias -- Alias is needed for derived table in standard SQL
    WHERE avg_salary > 42000;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 48: Subquery in the FROM clause with alias for relation and attributes

* **Purpose:** Same as Query 47, but explicitly names the derived table (`dept_avg`) and its columns (`dept_name`, `avg_salary`) using the `AS` clause.
* **Technique(s):** Subquery in `FROM` clause. Using `AS` to provide an alias for the derived table and rename its attributes.
* **Source Context:** Chapter 3, Section 3.8.5.
* **SQL Query:**
    ```sql
    SELECT dept_name, avg_salary
    FROM (SELECT dept_name, AVG(salary)
          FROM instructor
          GROUP BY dept_name) AS dept_avg (dept_name, avg_salary)
    WHERE avg_salary > 42000;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 49: Aggregate function on result of subquery in FROM clause

* **Purpose:** To find the maximum total salary budget across all departments.
* **Technique(s):** Subquery in `FROM` calculates the total salary (`SUM(salary)`) for each department using `GROUP BY`. The outer query then applies the `MAX()` aggregate function to the `tot_salary` column of this derived table.
* **Source Context:** Chapter 3, Section 3.8.5.
* **SQL Query:**
    ```sql
    SELECT MAX(tot_salary)
    FROM (SELECT dept_name, SUM(salary)
          FROM instructor
          GROUP BY dept_name) AS dept_total (dept_name, tot_salary);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 50: Correlated subquery in FROM clause using LATERAL

* **Purpose:** To print the name and salary of each instructor, along with the average salary of their specific department.
* **Technique(s):** `LATERAL` keyword used with a subquery in the `FROM` clause. Allows the subquery (`I2`) to reference columns from preceding items in the `FROM` list (`I1`). This enables calculating the department average dynamically for each instructor. (Note: `LATERAL` has limited support in SQL implementations).
* **Source Context:** Chapter 3, Section 3.8.5.
* **SQL Query:**
    ```sql
    SELECT name, salary, avg_salary
    FROM instructor I1, LATERAL (SELECT AVG(salary) AS avg_salary
                                 FROM instructor I2
                                 WHERE I2.dept_name = I1.dept_name);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 51: WITH clause for defining temporary views

* **Purpose:** To find the budget(s) of the department(s) with the maximum budget.
* **Technique(s):** `WITH` clause defines a temporary named relation (`max_budget`) containing the maximum budget value (Common Table Expression - CTE). The main query then joins the `department` table with this CTE to find departments matching the maximum budget. Improves readability compared to nested subqueries.
* **Source Context:** Chapter 3, Section 3.8.6.
* **SQL Query:**
    ```sql
    WITH max_budget (value) AS
      (SELECT MAX(budget)
       FROM department)
    SELECT budget
    FROM department, max_budget
    WHERE department.budget = max_budget.value;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 52: Multiple temporary views using WITH clause

* **Purpose:** To find all departments where the total salary is greater than the average of the total salaries across all departments.
* **Technique(s):** `WITH` clause used to define multiple CTEs: `dept_total` (calculating total salary per department) and `dept_total_avg` (calculating the average of those total salaries). The final query joins these CTEs to filter departments. Demonstrates modularity and readability benefits of `WITH`.
* **Source Context:** Chapter 3, Section 3.8.6.
* **SQL Query:**
    ```sql
    WITH dept_total (dept_name, value) AS
      (SELECT dept_name, SUM(salary)
       FROM instructor
       GROUP BY dept_name),
    dept_total_avg (value) AS
      (SELECT AVG(value)
       FROM dept_total)
    SELECT dept_name
    FROM dept_total, dept_total_avg
    WHERE dept_total.value >= dept_total_avg.value;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 53: Scalar subquery in SELECT clause

* **Purpose:** To list all department names along with the number of instructors in each department.
* **Technique(s):** Scalar subquery: a subquery used within the `SELECT` list that returns a single value (one row, one column). The subquery uses `COUNT(*)` and is correlated with the outer query via `department.dept_name = instructor.dept_name` to count instructors for the current department being processed by the outer query.
* **Source Context:** Chapter 3, Section 3.8.7.
* **SQL Query:**
    ```sql
    SELECT dept_name,
           (SELECT COUNT(*)
            FROM instructor
            WHERE department.dept_name = instructor.dept_name) AS num_instructors
    FROM department;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---

**--- Chapter 4 Queries ---**

### Query 54: Join with ON clause

* **Purpose:** To combine `student` and `takes` information based on matching `ID` values.
* **Technique(s):** Explicit `JOIN...ON` clause. The `ON` condition specifies the join predicate (`student.ID = takes.ID`). Unlike `NATURAL JOIN` or `USING`, common columns (`ID`) appear twice in the result unless explicitly projected. Functionally similar to using a `WHERE` clause for the join condition in this simple case.
* **Source Context:** Chapter 4, Section 4.1.1.
* **SQL Query:**
    ```sql
    SELECT *
    FROM student JOIN takes ON student.ID = takes.ID;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 55: Join with ON clause, explicit attribute selection and alias

* **Purpose:** Same join as Query 54, but explicitly lists the desired attributes in the `SELECT` clause to avoid duplicate `ID` columns and potentially rename `student.ID` to just `ID`.
* **Technique(s):** `JOIN...ON` clause. Explicit projection of columns in the `SELECT` list. Use of alias (`AS ID`) for the projected `student.ID`.
* **Source Context:** Chapter 4, Section 4.1.1.
* **SQL Query:**
    ```sql
    SELECT student.ID AS ID, name, dept_name, tot_cred,
           course_id, sec_id, semester, year, grade
    FROM student JOIN takes ON student.ID = takes.ID;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 56: Left Outer Join (Natural)

* **Purpose:** To list all students along with the courses they have taken, ensuring that students who have not taken any courses (like 'Snow') are still included in the result, with NULL values for the attributes from the `takes` relation [cite: 1100-1101, 1103].
* **Technique(s):** `NATURAL LEFT OUTER JOIN`. Preserves all tuples from the left relation (`student`). If a student tuple has no matching `takes` tuple based on `ID`, it's included in the result padded with NULLs for `takes` attributes.
* **Source Context:** Chapter 4, Section 4.1.2.
* **SQL Query:**
    ```sql
    SELECT *
    FROM student NATURAL LEFT OUTER JOIN takes;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 57: Left Outer Join used to find non-matching rows

* **Purpose:** To find the IDs of all students who have *not* taken any course.
* **Technique(s):** `NATURAL LEFT OUTER JOIN` between `student` and `takes`. The `WHERE course_id IS NULL` clause filters the result to include only those student tuples that had no match in `takes` (and were therefore padded with NULLs).
* **Source Context:** Chapter 4, Section 4.1.2.
* **SQL Query:**
    ```sql
    SELECT ID
    FROM student NATURAL LEFT OUTER JOIN takes
    WHERE course_id IS NULL;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 58: Right Outer Join (Natural)

* **Purpose:** To list all students and their taken courses, ensuring all students are included (similar to Query 56, but achieved by reversing table order and using `RIGHT OUTER JOIN`).
* **Technique(s):** `NATURAL RIGHT OUTER JOIN`. Preserves all tuples from the right relation (`student`). If a student tuple has no match in `takes`, it's included padded with NULLs for `takes` attributes. The result is semantically the same as the left outer join but with potentially different column order.
* **Source Context:** Chapter 4, Section 4.1.2.
* **SQL Query:**
    ```sql
    SELECT *
    FROM takes NATURAL RIGHT OUTER JOIN student;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 59: Full Outer Join (Natural) with subqueries in FROM

* **Purpose:** To display a list of all Comp. Sci. students along with any course sections they took in Spring 2009, AND ALSO display all Spring 2009 sections, even if no Comp. Sci. student took them.
* **Technique(s):** `NATURAL FULL OUTER JOIN`. Preserves tuples from *both* the left and right relations that do not have matches in the other relation, padding with NULLs as needed [cite: 1105, 1117-1118, 1128]. Uses subqueries in the `FROM` clause to pre-filter students (to Comp. Sci.) and takes (to Spring 2009) before the outer join.
* **Source Context:** Chapter 4, Section 4.1.2.
* **SQL Query:**
    ```sql
    SELECT *
    FROM (SELECT *
          FROM student
          WHERE dept_name = 'Comp. Sci.') AS cs_students -- Alias needed
    NATURAL FULL OUTER JOIN
         (SELECT *
          FROM takes
          WHERE semester = 'Spring' AND year = 2009) AS spring_takes; -- Alias needed
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 60: Left Outer Join with ON clause

* **Purpose:** To combine `student` and `takes` based on matching `ID` values, ensuring all students are included (similar to Query 56).
* **Technique(s):** `LEFT OUTER JOIN` with an explicit `ON` condition (`student.ID = takes.ID`). Preserves all tuples from the left relation (`student`), padding with NULLs where no match is found based on the `ON` condition. The common column (`ID`) appears twice in the raw result.
* **Source Context:** Chapter 4, Section 4.1.2.
* **SQL Query:**
    ```sql
    SELECT *
    FROM student LEFT OUTER JOIN takes ON student.ID = takes.ID;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 61: Illustrating difference between ON and WHERE in Outer Join

* **Purpose:** To demonstrate that moving a join predicate from the `ON` clause to the `WHERE` clause changes the semantics of an `OUTER JOIN`. This query is unlikely to produce the intended result of a standard left outer join.
* **Technique(s):** `LEFT OUTER JOIN` with a trivial `ON true` condition (conceptually joins every student with every takes record, padding non-matching students) followed by a `WHERE student.ID = takes.ID` filter [cite: 1147, 1149-1150]. The `WHERE` clause filters *after* the outer join padding, potentially eliminating the very NULL-padded rows the outer join was intended to preserve [cite: 1143-1145, 1151-1152].
* **Source Context:** Chapter 4, Section 4.1.2.
* **SQL Query:**
    ```sql
    SELECT *
    FROM student LEFT OUTER JOIN takes ON TRUE
    WHERE student.ID = takes.ID;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 62: Inner Join with USING clause

* **Purpose:** To combine `student` and `takes` information based on matching `ID` values, excluding students who haven't taken courses.
* **Technique(s):** `JOIN...USING(ID)`. Specifies the column (`ID`) to use for the join condition. Assumes `ID` exists in both tables. Only includes rows where a match is found (inner join behavior). The common column (`ID`) appears only once in the result. `INNER` keyword is optional.
* **Source Context:** Chapter 4, Section 4.1.3.
* **SQL Query:**
    ```sql
    SELECT *
    FROM student JOIN takes USING (ID);
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 63: Querying a view

* **Purpose:** To find all Physics courses offered in the Fall 2009 semester that were held in the Watson building, by querying a pre-defined view named `physics_fall_2009`.
* **Technique(s):** Using a view name (`physics_fall_2009`) in the `FROM` clause as if it were a base table. The database system replaces the view name with its underlying query definition during processing.
* **Source Context:** Chapter 4, Section 4.2.2.
* **SQL Query:**
    ```sql
    -- Assuming physics_fall_2009 view is defined as in Query 65
    SELECT course_id
    FROM physics_fall_2009
    WHERE building = 'Watson';
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here)*

---
### Query 64: Query used within a view definition (Example: faculty view)

* **Purpose:** This query forms the definition of the `faculty` view, intended to show instructor ID, name, and department, hiding the salary.
* **Technique(s):** Basic `SELECT` statement used within a `CREATE VIEW` command. Demonstrates using views for security/abstraction.
* **Source Context:** Chapter 4, Section 4.2.1.
* **SQL Query (as part of view definition):**
    ```sql
    -- CREATE VIEW faculty AS
    SELECT ID, name, dept_name
    FROM instructor;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here, if run standalone)*

---
### Query 65: Query used within a view definition (Example: physics_fall_2009 view)

* **Purpose:** This query forms the definition of the `physics_fall_2009` view, listing course sections offered by the Physics department in Fall 2009, including building and room number.
* **Technique(s):** Implicit join between `course` and `section` with filtering conditions in the `WHERE` clause. Used within a `CREATE VIEW` statement.
* **Source Context:** Chapter 4, Section 4.2.1 [cite: 1166-1167, 1185].
* **SQL Query (as part of view definition):**
    ```sql
    -- CREATE VIEW physics_fall_2009 AS
    SELECT course.course_id, sec_id, building, room_number
    FROM course, section
    WHERE course.course_id = section.course_id
      AND course.dept_name = 'Physics'
      AND section.semester = 'Fall'
      AND section.year = '2009';
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here, if run standalone)*

---
### Query 66: Query used within a view definition (Example: departments_total_salary view)

* **Purpose:** This query forms the definition of the `departments_total_salary` view, calculating the sum of instructor salaries for each department.
* **Technique(s):** Aggregate function `SUM()` with `GROUP BY` clause. Used within a `CREATE VIEW` statement that explicitly names the view attributes (`dept_name`, `total_salary`) because `SUM(salary)` doesn't have an inherent name.
* **Source Context:** Chapter 4, Section 4.2.2.
* **SQL Query (as part of view definition):**
    ```sql
    -- CREATE VIEW departments_total_salary(dept_name, total_salary) AS
    SELECT dept_name, SUM(salary)
    FROM instructor
    GROUP BY dept_name;
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here, if run standalone)*

---
### Query 67: Querying a view derived from another view (Example: physics_fall_2009_watson)

* **Purpose:** This query defines the `physics_fall_2009_watson` view by selecting specific columns from the `physics_fall_2009` view and filtering for the Watson building.
* **Technique(s):** Demonstrates view composition, where one view (`physics_fall_2009_watson`) is defined by querying another view (`physics_fall_2009`).
* **Source Context:** Chapter 4, Section 4.2.2.
* **SQL Query (as part of view definition):**
    ```sql
    -- CREATE VIEW physics_fall_2009_watson AS
    -- Assuming physics_fall_2009 view is defined as in Query 65
    SELECT course_id, room_number
    FROM physics_fall_2009
    WHERE building = 'Watson';
    ```
* **Output Screenshot:**
    * *(Insert screenshot of query output here, if run standalone)*

---

## 3. Conclusion

This documentation covers the specific SQL SELECT queries identified in Chapters 3 and 4 of the course textbook. The queries illustrate a range of SQL features, including various join types, aggregations, subqueries, set operations, and the use of views and common table expressions (WITH clause).

convert it in word file
