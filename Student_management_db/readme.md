
#  University Student Management System (Oracle SQL)

![Database ER Diagram](student_ERD.png)

A complete Oracle database solution for managing university students, courses, departments, and enrollments.

##  Table of Contents
- [Key Features](#-key-features)
- [Database Schema](#-database-schema)  
- [Relationships](#-relationships)
- [Installation](#-installation)  
- [Sample Data](#-sample-data)
- [Usage Examples](#-usage-examples)
- [Data Model](#-data-model)


##  Key Features

- **Department Management**  
  - Create and organize academic departments with locations.
- **Student Records**  
  - Store personal details with email uniqueness validation.
- **Instructor Management**  
  - Maintain faculty information with department assignments.
- **Course System**  
  - Manage course catalog with credit values.
  - Assign instructors to courses.
- **Enrollment Tracking**  
  - Record student enrollments with automatic date stamping.
  - Store grade information.

##  Database Schema

This is the schema Diagram of Student Management Database :

![Database Schema Diagram](images/schema.png)

##  Relationships


### 🔹 1. **Department → Students**
- **One-to-Many**  
  A department can have multiple students, but each student belongs to one department.  
  **FK**: `STUDENTS.DEPARTMENT_ID → DEPARTMENT.DEPARTMENT_ID`

---

### 🔹 2. **Department → Instructors**
- **One-to-Many**  
  A department can have multiple instructors, but each instructor is associated with one department.  
  **FK**: `INSTRUCTOR.DEPARTMENT_ID → DEPARTMENT.DEPARTMENT_ID`

---

### 🔹 3. **Department → Courses**
- **One-to-Many**  
  A department can offer multiple courses, but each course belongs to one department.  
  **FK**: `COURSES.DEPARTMENT_ID → DEPARTMENT.DEPARTMENT_ID`

---

### 🔹 4. **Instructor → Courses**
- **One-to-Many**  
  An instructor can teach multiple courses, but each course is assigned to one instructor.  
  **FK**: `COURSES.INSTRUCTOR_ID → INSTRUCTOR.INSTRUCTOR_ID`

---

### 🔹 5. **Student → Enrollments**
- **One-to-Many**  
  A student can enroll in multiple courses, but each enrollment record refers to one student.  
  **FK**: `ENROLLMENTS.STUDENT_ID → STUDENTS.STUDENT_ID`

---

### 🔹 6. **Course → Enrollments**
- **One-to-Many**  
  A course can have multiple students enrolled, but each enrollment record refers to one course.  
  **FK**: `ENROLLMENTS.COURSE_ID → COURSES.COURSE_ID`


##  Installation

##### Prerequisites
- Oracle Database 11g or later
- SQL*Plus or Oracle SQL Developer
- 50MB free storage space

### Setup Steps
1. Clone the repository:

```bash

   git clone https://github.com/yourusername/student-management-db.git
   cd student-management-db

 ```

2. Execute the SQL scripts:

```
-- Create tables
@schema.sql

-- Load sample data
@sample_data.sql

```
3. Verify installation:

```
SELECT *  FROM tab;

```

## Sample Data

### Department Records

![Database Dept Recordes](images/dept.png)


### Student Records

![Database std Recordes](images/std.png)


## Usage Examples

1. Get All Enrollments with Grades :

```
SELECT s.student_id, s.first_name, c.course_name, e.grade
FROM enrollments e
JOIN students s ON e.student_id = s.student_id
JOIN courses c ON e.course_id = c.course_id;

```

2. Find Courses Without Instructors :

```
SELECT course_id, course_name 
FROM courses
WHERE instructor_id IS NULL;
```
3. Department Enrollment Statistics :

```
SELECT d.dept_name, COUNT(e.enrollment_id) AS enrollments
FROM department d
LEFT JOIN courses c ON d.department_id = c.department_id
LEFT JOIN enrollments e ON c.course_id = e.course_id
GROUP BY d.dept_name;
```

## Data Model


View full ERD of this : [click here](student_ERD.pdf)


| Constraint            | Description                          |
|-----------------------|--------------------------------------|
| `PK_*`                | Primary keys on all ID columns       |
| `FK_STUDENT_DEPT`     | Students → Department linkage        |
| `FK_COURSE_INSTRUCTOR`| Courses → Instructor relationship    |
| `EMAIL_UNIQUE`        | Unique email constraints             |
