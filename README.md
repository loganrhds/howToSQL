# howToSQL Example


CREATE SCHEMA `devcamp_sql_project` ;

CREATE TABLE `devcamp_sql_project`.`students` (
  `students_id` INT NOT NULL AUTO_INCREMENT,
  `students_name` VARCHAR(100) NOT NULL,
  `students_email` VARCHAR(80) NOT NULL,
  PRIMARY KEY (`students_id`),
  UNIQUE INDEX `students_id_UNIQUE` (`students_id` ASC) VISIBLE);
  
CREATE TABLE `devcamp_sql_project`.`courses` (
  `courses_id` INT NOT NULL AUTO_INCREMENT,
  `courses_name` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`courses_id`),
  UNIQUE INDEX `courses_id_UNIQUE` (`courses_id` ASC) VISIBLE);

CREATE TABLE `devcamp_sql_project`.`professors` (
  `professors_id` INT NOT NULL AUTO_INCREMENT,
  `professors_name` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`professors_id`),
  UNIQUE INDEX `professors_id_UNIQUE` (`professors_id` ASC) VISIBLE);
  
CREATE TABLE `devcamp_sql_project`.`grades` (
  `grades_id` INT NOT NULL AUTO_INCREMENT,
  `grades_grade_percentage` VARCHAR(45) NOT NULL,
  `grades_courses_id` INT NULL,
  `grades_professors_id` INT NULL,
  `grades_students_id` INT NULL,
  PRIMARY KEY (`grades_id`),
  UNIQUE INDEX `grades_id_UNIQUE` (`grades_id` ASC) VISIBLE,
  INDEX `grades_courses_id_idx` (`grades_courses_id` ASC) VISIBLE,
  INDEX `grades_professors_id_idx` (`grades_professors_id` ASC) VISIBLE,
  INDEX `grades_students_id_idx` (`grades_students_id` ASC) VISIBLE,
  CONSTRAINT `grades_courses_id`
    FOREIGN KEY (`grades_courses_id`)
    REFERENCES `devcamp_sql_project`.`courses` (`courses_id`)
    ON DELETE NO ACTION
    ON UPDATE CASCADE,
  CONSTRAINT `grades_professors_id`
    FOREIGN KEY (`grades_professors_id`)
    REFERENCES `devcamp_sql_project`.`professors` (`professors_id`)
    ON DELETE CASCADE
    ON UPDATE NO ACTION,
  CONSTRAINT `grades_students_id`
    FOREIGN KEY (`grades_students_id`)
    REFERENCES `devcamp_sql_project`.`students` (`students_id`)
    ON DELETE CASCADE
    ON UPDATE NO ACTION);


USE devcamp_sql_project;

INSERT INTO students(students_name, students_email)
VALUES ('Jim', 'jim@test.com');

INSERT INTO students(students_name, students_email)
VALUES ('Jim1', 'jim1@test.com');

INSERT INTO students(students_name, students_email)
VALUES ('Jim2', 'jim2@test.com');

INSERT INTO students(students_name, students_email)
VALUES ('Jim3', 'jim3@test.com');

INSERT INTO students(students_name, students_email)
VALUES ('Jim4', 'jim4@test.com');

INSERT INTO professors(professors_name)
VALUES ('ProfessorX');

INSERT INTO professors(professors_name)
VALUES ('ProfessorX1');

INSERT INTO professors(professors_name)
VALUES ('ProfessorX2');

INSERT INTO courses(courses_name)
VALUES ('CS101');

INSERT INTO courses(courses_name)
VALUES ('CS102');

INSERT INTO courses(courses_name)
VALUES ('CS103');

INSERT INTO grades(grades_grade_percentage, grades_courses_id, grades_professors_id, grades_students_id)
VALUES (75.00, 1, 1, 1);

INSERT INTO grades(grades_grade_percentage, grades_courses_id, grades_professors_id, grades_students_id)
VALUES (85.00, 1, 1, 1);

INSERT INTO grades(grades_grade_percentage, grades_courses_id, grades_professors_id, grades_students_id)
VALUES (55.00, 2, 2, 2);

INSERT INTO grades(grades_grade_percentage, grades_courses_id, grades_professors_id, grades_students_id)
VALUES (65.00, 2, 2, 2);

INSERT INTO grades(grades_grade_percentage, grades_courses_id, grades_professors_id, grades_students_id)
VALUES (57.00, 3, 3, 3);

INSERT INTO grades(grades_grade_percentage, grades_courses_id, grades_professors_id, grades_students_id)
VALUES (67.00, 3, 3, 3);

INSERT INTO grades(grades_grade_percentage, grades_courses_id, grades_professors_id, grades_students_id)
VALUES (77.00, 2, 2, 4);

INSERT INTO grades(grades_grade_percentage, grades_courses_id, grades_professors_id, grades_students_id)
VALUES (87.00, 1, 1, 4);

INSERT INTO grades(grades_grade_percentage, grades_courses_id, grades_professors_id, grades_students_id)
VALUES (97.00, 2, 2, 5);

INSERT INTO grades(grades_grade_percentage, grades_courses_id, grades_professors_id, grades_students_id)
VALUES (65.00, 3, 3, 1);

SELECT AVG(grades_grade_percentage)
FROM grades g
JOIN professors p
ON g.grades_professors_id = p.professors_id
WHERE p.professors_name = "ProfessorX";

SELECT MAX(grades_grade_percentage), s.students_name
FROM grades g
JOIN students s
ON g.grades_students_id = s.students_id
WHERE s.students_name = "Jim";

SELECT s.students_name, c.courses_name
FROM students s
JOIN grades g
ON g.grades_students_id = s.students_id
JOIN courses c
ON c.courses_id = g.grades_courses_id;

SELECT courses_name, AVG(grades_grade_percentage)
FROM grades g
JOIN courses c
ON g.grades_courses_id = c.courses_id
WHERE c.courses_name = "CS101";



