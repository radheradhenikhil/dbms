# Name: Nikhil Agarwal
# Roll no.: 30712389613
# Database Management System BCA-4002

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
    * *![image](https://github.com/user-attachments/assets/4b35ebfb-21d6-4edf-a49f-619f3bb5ac8c)
*

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
    * *![image](https://github.com/user-attachments/assets/482acf96-e553-46c9-b88c-3a38e4083be5)
*

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
    * *![image](https://github.com/user-attachments/assets/275ec56e-0635-4282-9ee8-a4f74593db08)
*

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
    * ![image](https://github.com/user-attachments/assets/7c3b44be-6b3d-4a96-b491-e9c6af640bf8)


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
    * ![image](https://github.com/user-attachments/assets/893a0947-01ab-4a60-8996-2c17b50598b2)


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
    * ![image](https://github.com/user-attachments/assets/8375b686-292a-47f1-9da5-48272c2a30f2)

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
    * ![image](https://github.com/user-attachments/assets/c67b7a2d-aa1b-46b2-bf81-1e1022d6f65c)


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
    * ![image](https://github.com/user-attachments/assets/df45d3b5-2221-4152-bc51-aa3963149e43)

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
    * ![image](https://github.com/user-attachments/assets/ecc227b8-7c86-49e4-a5d4-4c2a6267b843)


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
    * ![image](https://github.com/user-attachments/assets/1c0b6b10-9a90-4995-8930-1581e04285cc)

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
    * ![image](https://github.com/user-attachments/assets/86e909e7-e7ae-4311-a9e3-d52787e982bb)


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
    * ![image](https://github.com/user-attachments/assets/733a8866-4a0a-4415-babf-2497afef7bb8)

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
    * ![image](https://github.com/user-attachments/assets/33be61ab-7272-4dea-a6ae-af150ac88a1c)


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
    * ![image](https://github.com/user-attachments/assets/c80af514-e1ad-4ee4-a7d8-9498f1bb9f6d)


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
    * ![image](https://github.com/user-attachments/assets/65fb2a2c-a3e1-4d4c-b2de-0acc7751d41e)


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
    * ![image](https://github.com/user-attachments/assets/d1fc16bc-9c86-4483-8669-9c2f1eef7881)

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
    * ![image](https://github.com/user-attachments/assets/2ea5d2b4-9f29-46d9-82f4-fae81ac2f651)

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
    * ![image](https://github.com/user-attachments/assets/145d1cf7-26d1-41a3-93b9-24553d468a90)

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
    * ![image](https://github.com/user-attachments/assets/161a8955-4069-4213-890c-c8b25cdec702)

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
    * ![image](https://github.com/user-attachments/assets/3fa22547-0c2c-43ac-a4d2-4655cf37b69c)


---
### Query 21: Checking for NULL values

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
    * ![image](https://github.com/user-attachments/assets/76f877fb-c112-47b8-abba-578d2b734adb)


---
### Query 22: Aggregate function AVG

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
    * ![image](https://github.com/user-attachments/assets/c80bc340-16e2-4fea-8d9a-2104b074a748)

---
### Query 23: Aggregate function AVG with Alias

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
    * ![image](https://github.com/user-attachments/assets/60665a19-7383-45d5-953b-bd6afb52876f)


---
### Query 24: Aggregate function COUNT DISTINCT

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
    * ![image](https://github.com/user-attachments/assets/20060f6c-e7fa-41a1-89b0-d3a8c60d3597)


---
### Query 25: Aggregate function COUNT(*)

* **Purpose:** To find the total number of tuples (rows) in the `course` relation.
* **Technique(s):** `COUNT(*)` aggregate function. Counts all rows in the result set defined by the `FROM` and `WHERE` clauses (or the entire table if no `WHERE` clause).
* **Source Context:** Chapter 3, Section 3.7.1.
* **SQL Query:**
    ```sql
    SELECT COUNT(*)
    FROM course;
    ```
* **Output Screenshot:**
    * ![image](https://github.com/user-attachments/assets/afa4f82c-c1ee-4f95-9e38-5f6654a90bce)


---
### Query 26: Aggregate function with GROUP BY

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
    * ![image](https://github.com/user-attachments/assets/284b9aa5-b138-4a90-9d88-adf22ad93cb3)

---
### Query 27: Aggregate function with GROUP BY and JOIN

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
    * ![image](https://github.com/user-attachments/assets/2a51a432-05e7-4720-b76e-c16dbcbe135e)


---
### Query 28: HAVING clause to filter groups

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
    * ![image](https://github.com/user-attachments/assets/d9d7498b-e488-464b-b575-3f836215a118)

---
### Query 29: GROUP BY multiple columns with HAVING clause

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
    * ![image](https://github.com/user-attachments/assets/1f6a7664-5543-48d0-bbf5-0880d51c46c4)


---
### Query 30: Aggregate SUM (handles NULLs)

* **Purpose:** To calculate the total salary expenditure for all instructors.
* **Technique(s):** `SUM()` aggregate function. Ignores NULL values in the input collection by default.
* **Source Context:** Chapter 3, Section 3.7.4.
* **SQL Query:**
    ```sql
    SELECT SUM(salary)
    FROM instructor;
    ```
* **Output Screenshot:**
    * ![image](https://github.com/user-attachments/assets/064f6334-915d-4edd-8916-807538009c53)


---
### Query 31: Subquery with IN operator

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
    * ![image](https://github.com/user-attachments/assets/19f25bac-21b6-47ab-bfcf-5152c981bd30)

---
### Query 32: Subquery with NOT IN operator

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
    * ![image](https://github.com/user-attachments/assets/714f5734-0446-440e-8abd-cf0d80613270)

---
### Query 33: NOT IN with an enumerated list

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
    * ![image](https://github.com/user-attachments/assets/c292f721-9200-4692-a5dc-b39122505e97)


---
### Query 34: Subquery with tuple comparison using IN

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
    * ![image](https://github.com/user-attachments/assets/75995277-6bc5-4463-aed3-afb36706086b)


---
### Query 35: Subquery with > SOME comparison

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
    * ![image](https://github.com/user-attachments/assets/86beec8d-f6a2-443d-857e-3d90ae0d2cdf)

---
### Query 36: Subquery with > ALL comparison

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
    * ![image](https://github.com/user-attachments/assets/c5c2b42a-1b88-48bb-bdc8-09736ff78cf4)

---
### Query 37: Subquery with >= ALL comparison (finding maximum)

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
    * ![image](https://github.com/user-attachments/assets/0ce48d6e-c552-42fd-99a9-2f0348d50689)

---
### Query 38: Correlated subquery with EXISTS

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
    * ![image](https://github.com/user-attachments/assets/f16a6303-69d3-48f3-9c7d-0a4b3567b252)


---

### Query 39: Subquery in the FROM clause with alias for relation and attributes

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
    * ![image](https://github.com/user-attachments/assets/526e3c43-4bfe-4c9b-a57a-a75d9fffce56)

---
### Query 40: Aggregate function on result of subquery in FROM clause

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
    * ![image](https://github.com/user-attachments/assets/08969d11-221c-4cc5-8c79-f33b417295db)


---
### Query 41: WITH clause for defining temporary views

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
    * ![image](https://github.com/user-attachments/assets/265ea9bf-2ca8-4bff-b1c5-135aac44a7ef)


---
### Query 42: Multiple temporary views using WITH clause

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
    * ![image](https://github.com/user-attachments/assets/cc9d9291-101a-4301-8003-3b0babee634d)

---
### Query 43: Scalar subquery in SELECT clause

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
    * ![image](https://github.com/user-attachments/assets/f23a0d29-e488-42f1-b41f-e1567b2ba09a)

---

**--- Chapter 4 Queries ---**

### Query 44: Join with ON clause

* **Purpose:** To combine `student` and `takes` information based on matching `ID` values.
* **Technique(s):** Explicit `JOIN...ON` clause. The `ON` condition specifies the join predicate (`student.ID = takes.ID`). Unlike `NATURAL JOIN` or `USING`, common columns (`ID`) appear twice in the result unless explicitly projected. Functionally similar to using a `WHERE` clause for the join condition in this simple case.
* **Source Context:** Chapter 4, Section 4.1.1.
* **SQL Query:**
    ```sql
    SELECT *
    FROM student JOIN takes ON student.ID = takes.ID;
    ```
* **Output Screenshot:**
    * ![image](https://github.com/user-attachments/assets/be400e2e-89b8-489b-bf13-aa75e58fdeb2)


---
### Query 45: Join with ON clause, explicit attribute selection and alias

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
    * ![image](https://github.com/user-attachments/assets/2cb7f14f-dc6a-40ec-9650-fd481b6849b2)


---
### Query 46: Left Outer Join (Natural)

* **Purpose:** To list all students along with the courses they have taken, ensuring that students who have not taken any courses (like 'Snow') are still included in the result, with NULL values for the attributes from the `takes` relation [cite: 1100-1101, 1103].
* **Technique(s):** `NATURAL LEFT OUTER JOIN`. Preserves all tuples from the left relation (`student`). If a student tuple has no matching `takes` tuple based on `ID`, it's included in the result padded with NULLs for `takes` attributes.
* **Source Context:** Chapter 4, Section 4.1.2.
* **SQL Query:**
    ```sql
    SELECT *
    FROM student NATURAL LEFT OUTER JOIN takes;
    ```
* **Output Screenshot:**
    * ![image](https://github.com/user-attachments/assets/e7f470a7-5220-47a6-aaae-46e77625b70a)

---
### Query 47: Left Outer Join used to find non-matching rows

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
    * ![image](https://github.com/user-attachments/assets/bf19c3f3-006c-4c2e-9a92-3ee84a5a8266)


---
### Query 48: Right Outer Join (Natural)

* **Purpose:** To list all students and their taken courses, ensuring all students are included (similar to Query 56, but achieved by reversing table order and using `RIGHT OUTER JOIN`).
* **Technique(s):** `NATURAL RIGHT OUTER JOIN`. Preserves all tuples from the right relation (`student`). If a student tuple has no match in `takes`, it's included padded with NULLs for `takes` attributes. The result is semantically the same as the left outer join but with potentially different column order.
* **Source Context:** Chapter 4, Section 4.1.2.
* **SQL Query:**
    ```sql
    SELECT *
    FROM takes NATURAL RIGHT OUTER JOIN student;
    ```
* **Output Screenshot:**
    * ![image](https://github.com/user-attachments/assets/5cf15184-9e00-451a-9f44-f9df887fc180)


---
### Query 49: Left Outer Join with ON clause

* **Purpose:** To combine `student` and `takes` based on matching `ID` values, ensuring all students are included (similar to Query 56).
* **Technique(s):** `LEFT OUTER JOIN` with an explicit `ON` condition (`student.ID = takes.ID`). Preserves all tuples from the left relation (`student`), padding with NULLs where no match is found based on the `ON` condition. The common column (`ID`) appears twice in the raw result.
* **Source Context:** Chapter 4, Section 4.1.2.
* **SQL Query:**
    ```sql
    SELECT *
    FROM student LEFT OUTER JOIN takes ON student.ID = takes.ID;
    ```
* **Output Screenshot:**
    * ![image](https://github.com/user-attachments/assets/feea0c73-f8ac-45f1-ad73-9f78d38de7ef)

---
### Query 50: Illustrating difference between ON and WHERE in Outer Join

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
    * ![image](https://github.com/user-attachments/assets/cf9edceb-7f62-41e4-8db2-26ffe1895755)


---
### Query 51: Inner Join with USING clause

* **Purpose:** To combine `student` and `takes` information based on matching `ID` values, excluding students who haven't taken courses.
* **Technique(s):** `JOIN...USING(ID)`. Specifies the column (`ID`) to use for the join condition. Assumes `ID` exists in both tables. Only includes rows where a match is found (inner join behavior). The common column (`ID`) appears only once in the result. `INNER` keyword is optional.
* **Source Context:** Chapter 4, Section 4.1.3.
* **SQL Query:**
    ```sql
    SELECT *
    FROM student JOIN takes USING (ID);
    ```
* **Output Screenshot:**
    * ![image](https://github.com/user-attachments/assets/5c76060f-34f0-4462-8098-27e0caeba762)



---
### Query 52: Query used within a view definition (Example: faculty view)

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
    * ![image](https://github.com/user-attachments/assets/83e2d4e9-46b3-4018-bea4-56764b7afac0)


---
### Query 53: Query used within a view definition (Example: physics_fall_2009 view)

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
    * ![image](https://github.com/user-attachments/assets/1246b96e-8cb3-4bc1-9fd0-90215436b8b6)


---
### Query 54: Query used within a view definition (Example: departments_total_salary view)

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
    * ![image](https://github.com/user-attachments/assets/41a80b54-5513-4b5c-b215-d992749cb47d)


---
