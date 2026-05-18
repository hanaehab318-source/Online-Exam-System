# Online Examination System - SQL Project

## Project Description
This project represents an Online Examination System database designed using SQL.  
The system helps manage users, exams, questions, choices, answers, and results.

The database includes:
- Tables
- Relationships
- Insert, Select, Update, Delete operations
- ALTER statement
- Views
- Functions
- Stored Procedures

---

# Database Name
OnlineExamSystem

---

# Tables Used

## 1. Users
Stores users information.

### Columns:
- user_id
- name
- email
- role

---

## 2. Exams
Stores exams information.

### Columns:
- exam_id
- title
- description
- exam_date
- duration

---

## 3. Questions
Stores exam questions.

### Columns:
- question_id
- exam_id
- question_text
- marks

---

## 4. Choices
Stores question choices.

### Columns:
- choice_id
- question_id
- choice_text
- is_correct

---

## 5. Answers
Stores student answers.

### Columns:
- answer_id
- user_id
- question_id
- selected_choice

---

## 6. Results
Stores students results and scores.

### Columns:
- result_id
- user_id
- exam_id
- score

---

# Relationships
- One Exam has many Questions.
- One Question has many Choices.
- One User can answer many Questions.
- One User can have many Results.

Foreign Keys were used to connect tables together.

---

# SQL Operations Used

## CREATE
Used to create:
- Database
- Tables

---

## INSERT
Used to add new records into tables.

Example:
```sql
INSERT INTO Users (name, email, role)
VALUES ('Hana Ehab', 'hana@gmail.com', 'Student');
