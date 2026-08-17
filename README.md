# This is a College Management System
This repository contains the SQL scripts to initialize and build a relational database schema named 'college_demo'.
It demonstrates fundamental database design constraints such as Primary Keys, Foreign Keys, Unique constraints, and Composite Keys.
## SQL Commands & Schema Breakdown
### 1. Database Initialization
* **'CREATE DATABASE college_demo;'** -Creates a new separate database container named 'college_demo'.
* **'USE college_demo;'** -Instructs MYSQL to execute all subsequent table commands inside this specific database.
---
  ### 2. Department Table('department')
  This is the parent lookup table for academic departments.
  #### Sample Data:
dept_id	dept_name
1	Computer Science     
2	Electronics          
<img width="241" height="73" alt="image" src="https://github.com/user-attachments/assets/75c68ff7-af5d-4aa0-a666-0ed65bede863" />
#### Structural Rules:
* **'dept_id INT PRIMARY KEY'** - Uniquely identifies each department; cannot be null.
* **'dept_name VARCHAR(50) UNIQUE NOT NULL'** -Stores the department name. It is mandatory ('NOT NULL') and
  prevents duplicate department names ('UNIQUE'), making it an **Alternate Key**.
---
### 3. Student Table (student)
Stores student profiles and links them to their respective departments.
##### Sample Data:
roll_no	name	email	aadhar_no	dept_id
101	Nilisha	nilisha@mail.com	123456780012.00	1
102	Rahul	rahul@mail.com	987654321098.00	2
<img width="572" height="73" alt="image" src="https://github.com/user-attachments/assets/a213f543-cf23-4c83-92e5-ca9fbde57aa8" />
#### Structural Rules:
* **'roll_no INT PRIMARY KEY'** - Unique identifier for each individual student.
* **'name VARCHAR(50) NOT NULL'** - Ensures every student record has a name.
* **'email VARCHAR(50) UNIQUE'** - Prevents multiple students from registering with the identical email address.
* **'aadhar_no VARCHAR(12) UNIQUE'** - Validates and holds 12-digit government identification uniquely per student.
* **'FOREIGN KEY (dept_id) REFERENCES department(dept_id)'** - Establishes a relationship ensuring a student can only belong to a valid
  department already existing in the department table.
---
### 4. Course Table (course)

Contains details about classes offered.

#### Sample Data:
course_id	course_name	dept_id
501	DBMS	1
502	Circuits	2
<img width="241" height="73" alt="image" src="https://github.com/user-attachments/assets/ca791c56-e6dd-4ac1-96d3-730b719868ac" />
#### Structural Rules:
* **'course_id INT PRIMARY KEY'** - Unique identification key for each course.
* **'course_name VARCHAR(50) NOT NULL'** - Requires a name string for every course record.
* **'FOREIGN KEY (dept_id) REFERENCES department(dept_id)'** - Links the course back to the specific department managing it.
---
### 5. Enrollment Table (enrollment)

A junction table mapping the many-to-many relationship between students and courses.

#### Sample Data:
roll_no	course_id	semester	grade
101	501	3	A
101	502	3	B
101	502	4	B
<img width="321" height="97" alt="image" src="https://github.com/user-attachments/assets/cfcb576b-6f23-4496-a567-91cc3dc5c0cc" />
#### Structural Rules:
* **'PRIMARY KEY (roll_no, course_id, semester)'** - A *Composite Primary Key* combining three columns to ensure a student cannot enroll in the exact same class twice during the same semester.
* **'CHECK (semester BETWEEN 1 AND 8)'** - A validation rule that restricts entries only to standard college semesters (1 through 8).
* **'FOREIGN KEY (roll_no) REFERENCES student(roll_no)'** - Ensures the enrollment belongs to a real, registered student.
* **'FOREIGN KEY (course_id) REFERENCES course(course_id)'** - Ensures the student is enrolling in a real, existing course.


