# University Registration Database (Normalization using MySQL)

## Aim
The aim of this assignment is to normalize a university registration
database using First Normal Form (1NF), Second Normal Form (2NF),
and Third Normal Form (3NF) and implement it using MySQL.

---

## Functional Dependencies
- StudentID determines Name, Email, and Major
- Major determines Advisor
- CourseID determines CourseTitle, Credits, Building, and Room
- StudentID and CourseID together determine Grade

---

## Normalization Steps

### First Normal Form (1NF)
All columns contain single values and there are no repeating fields.
So the table already follows 1NF.

### Second Normal Form (2NF)
Partial dependency was removed by separating student information
and course information into different tables.

### Third Normal Form (3NF)
The dependency between Major and Advisor was removed by creating
a separate Majors table.

---

## Tables after Normalization
- Majors (Major, Advisor)
- Students (StudentID, Name, Email, Major)
- Courses (CourseID, CourseTitle, Credits, Building, Room)
- Enrollments (StudentID, CourseID, Grade)

---

## SQL Commands Used

### Create Database
```sql
CREATE DATABASE university_db;
USE university_db;


```sql
CREATE TABLE Majors (
    Major VARCHAR(50) PRIMARY KEY,
    Advisor VARCHAR(100) NOT NULL
);

CREATE TABLE Students (
    StudentID VARCHAR(10) PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    Major VARCHAR(50),
    FOREIGN KEY (Major) REFERENCES Majors(Major)
);

CREATE TABLE Courses (
    CourseID VARCHAR(10) PRIMARY KEY,
    CourseTitle VARCHAR(100) NOT NULL,
    Credits INT NOT NULL,
    Building VARCHAR(50),
    Room VARCHAR(10)
);

CREATE TABLE Enrollments (
    StudentID VARCHAR(10),
    CourseID VARCHAR(10),
    Grade CHAR(1),
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);
```
```sql
INSERT INTO Majors VALUES
('CS', 'Dr. Smith'),
('Physics', 'Dr. Lee');

INSERT INTO Students VALUES
('S101', 'Alice', 'alice@uni.edu', 'CS'),
('S102', 'Bob', 'bob@uni.edu', 'CS'),
('S103', 'Carol', 'carol@uni.edu', 'Physics');

INSERT INTO Courses VALUES
('CS301', 'Algorithms', 4, 'Science', '205'),
('MATH201', 'Linear Algebra', 3, 'Math Wing', '101'),
('PHYS101', 'Mechanics', 4, 'Science', '301');

INSERT INTO Enrollments VALUES
('S101', 'CS301', 'A'),
('S101', 'MATH201', 'B'),
('S102', 'CS301', 'C'),
('S103', 'PHYS101', 'A');

```
