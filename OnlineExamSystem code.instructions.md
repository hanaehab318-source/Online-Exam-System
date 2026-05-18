CREATE DATABASE OnlineExamSystem;
USE OnlineExamSystem;

-- Users Table
CREATE TABLE Users (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    role VARCHAR(50)
);

-- Exams Table
CREATE TABLE Exams (
    exam_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100),
    description TEXT,
    exam_date DATE,
    duration INT
);

-- Questions Table
CREATE TABLE Questions (
    question_id INT PRIMARY KEY AUTO_INCREMENT,
    exam_id INT,
    question_text TEXT,
    marks INT,
    FOREIGN KEY (exam_id) REFERENCES Exams(exam_id)
);

-- Choices Table
CREATE TABLE Choices (
    choice_id INT PRIMARY KEY AUTO_INCREMENT,
    question_id INT,
    choice_text VARCHAR(255),
    is_correct BOOLEAN,
    FOREIGN KEY (question_id) REFERENCES Questions(question_id)
);

-- Answers Table
CREATE TABLE Answers (
    answer_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    question_id INT,
    selected_choice INT,
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (question_id) REFERENCES Questions(question_id),
    FOREIGN KEY (selected_choice) REFERENCES Choices(choice_id)
);

-- Results Table
CREATE TABLE Results (
    result_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    exam_id INT,
    score DECIMAL(5,2),
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (exam_id) REFERENCES Exams(exam_id)
);

-- INSERT
INSERT INTO Users (name, email, role)
VALUES
('Hana Ehab', 'hana@gmail.com', 'Student'),
('Ahmed Ali', 'ahmed@gmail.com', 'Student');

INSERT INTO Exams (title, description, exam_date, duration)
VALUES
('Database Exam', 'SQL Basics Exam', '2026-05-20', 60);

INSERT INTO Questions (exam_id, question_text, marks)
VALUES
(1, 'What does SQL stand for?', 5);

INSERT INTO Choices (question_id, choice_text, is_correct)
VALUES
(1, 'Structured Query Language', TRUE),
(1, 'Simple Query Language', FALSE);

-- SELECT
SELECT * FROM Users;

SELECT * FROM Exams;

SELECT question_text, marks
FROM Questions;

-- UPDATE
UPDATE Users
SET email = 'hanaehab@gmail.com'
WHERE user_id = 1;

-- DELETE
DELETE FROM Choices
WHERE choice_id = 2;

-- ALTER
ALTER TABLE Users
ADD phone VARCHAR(20);

-- VIEW
CREATE VIEW StudentResults AS
SELECT 
    Users.name,
    Exams.title,
    Results.score
FROM Results
JOIN Users ON Results.user_id = Users.user_id
JOIN Exams ON Results.exam_id = Exams.exam_id;

-- SELECT FROM VIEW
SELECT * FROM StudentResults;

-- FUNCTION
DELIMITER $$

CREATE FUNCTION GetTotalMarks(exam INT)
RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE total INT;

    SELECT SUM(marks)
    INTO total
    FROM Questions
    WHERE exam_id = exam;

    RETURN total;
END $$

DELIMITER ;

-- CALL FUNCTION
SELECT GetTotalMarks(1);

-- STORED PROCEDURE
DELIMITER $$

CREATE PROCEDURE AddNewUser(
    IN u_name VARCHAR(100),
    IN u_email VARCHAR(100),
    IN u_role VARCHAR(50)
)
BEGIN
    INSERT INTO Users(name, email, role)
    VALUES(u_name, u_email, u_role);
END $$

DELIMITER ;

-- CALL STORED PROCEDURE
CALL AddNewUser('Donia Galal', 'donia@gmail.com', 'Student');
