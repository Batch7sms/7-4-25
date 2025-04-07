```sql
CREATE TABLE branches (
id int NOT NULL AUTO_INCREMENT,
name varchar(50) NOT NULL,
PRIMARY KEY (id),
UNIQUE KEY name (name)
) ENGINE=InnoDB AUTO_INCREMENT=25 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE attendance (
id int NOT NULL AUTO_INCREMENT,
student_id int DEFAULT NULL,
subject_id int DEFAULT NULL,
semester_id int DEFAULT NULL,
date date NOT NULL,
status enum('Present','Absent') NOT NULL,
PRIMARY KEY (id),
KEY student_id (student_id),
KEY subject_id (subject_id),
KEY semester_id (semester_id),
CONSTRAINT attendance_ibfk_1 FOREIGN KEY (student_id) REFERENCES students (id),
CONSTRAINT attendance_ibfk_2 FOREIGN KEY (subject_id) REFERENCES subjects (id),
CONSTRAINT attendance_ibfk_3 FOREIGN KEY (semester_id) REFERENCES semesters (id)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE regulations (
id int NOT NULL AUTO_INCREMENT,
name varchar(50) NOT NULL,
PRIMARY KEY (id),
UNIQUE KEY name (name)
) ENGINE=InnoDB AUTO_INCREMENT=23 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE semester_updates (
id int NOT NULL AUTO_INCREMENT,
branch_id int NOT NULL,
branch_name varchar(100) NOT NULL,
excluded_roll_numbers text,
updated_at timestamp NULL DEFAULT CURRENT_TIMESTAMP,
PRIMARY KEY (id),
KEY branch_id (branch_id),
CONSTRAINT semester_updates_ibfk_1 FOREIGN KEY (branch_id) REFERENCES branches (id) ON DELETE CASCADE
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE semesters (
id int NOT NULL AUTO_INCREMENT,
name varchar(50) NOT NULL,
PRIMARY KEY (id),
UNIQUE KEY name (name)
) ENGINE=InnoDB AUTO_INCREMENT=9 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE students (
id int NOT NULL AUTO_INCREMENT,
roll_number varchar(20) NOT NULL,
username varchar(50) NOT NULL,
full_name varchar(100) NOT NULL,
date_of_birth date NOT NULL,
aadhar_number varchar(20) DEFAULT NULL,
email varchar(100) NOT NULL,
mobile_number varchar(15) NOT NULL,
address text NOT NULL,
regulation_id int NOT NULL,
semester_id int NOT NULL,
branch_id int NOT NULL,
PRIMARY KEY (id),
UNIQUE KEY roll_number (roll_number),
UNIQUE KEY username (username),
UNIQUE KEY email (email),
UNIQUE KEY mobile_number (mobile_number),
UNIQUE KEY aadhar_number (aadhar_number),
KEY regulation_id (regulation_id),
KEY semester_id (semester_id),
KEY branch_id (branch_id),
CONSTRAINT students_ibfk_1 FOREIGN KEY (username) REFERENCES users (username) ON DELETE CASCADE,
CONSTRAINT students_ibfk_2 FOREIGN KEY (email) REFERENCES users (email) ON DELETE CASCADE,
CONSTRAINT students_ibfk_3 FOREIGN KEY (regulation_id) REFERENCES regulations (id) ON DELETE CASCADE,
CONSTRAINT students_ibfk_4 FOREIGN KEY (semester_id) REFERENCES semesters (id) ON DELETE CASCADE,
CONSTRAINT students_ibfk_5 FOREIGN KEY (branch_id) REFERENCES branches (id) ON DELETE CASCADE
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE subjects (
id int NOT NULL AUTO_INCREMENT,
subject_name varchar(100) NOT NULL,
regulation_id int DEFAULT NULL,
semester_id int DEFAULT NULL,
branch_id int DEFAULT NULL,
PRIMARY KEY (id),
UNIQUE KEY unique_subject (subject_name,regulation_id,semester_id,branch_id),
KEY regulation_id (regulation_id),
KEY semester_id (semester_id),
KEY branch_id (branch_id),
CONSTRAINT subjects_ibfk_1 FOREIGN KEY (regulation_id) REFERENCES regulations (id) ON DELETE CASCADE,
CONSTRAINT subjects_ibfk_2 FOREIGN KEY (semester_id) REFERENCES semesters (id) ON DELETE CASCADE,
CONSTRAINT subjects_ibfk_3 FOREIGN KEY (branch_id) REFERENCES branches (id) ON DELETE CASCADE
) ENGINE=InnoDB AUTO_INCREMENT=38 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE teacher_subjects (
id int NOT NULL AUTO_INCREMENT,
subject_id int DEFAULT NULL,
teacher_id int DEFAULT NULL,
PRIMARY KEY (id),
KEY subject_id (subject_id),
KEY teacher_id (teacher_id),
CONSTRAINT teacher_subjects_ibfk_1 FOREIGN KEY (subject_id) REFERENCES subjects (id) ON DELETE CASCADE,
CONSTRAINT teacher_subjects_ibfk_2 FOREIGN KEY (teacher_id) REFERENCES users (id) ON DELETE CASCADE
) ENGINE=InnoDB AUTO_INCREMENT=16 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE users (
id int NOT NULL AUTO_INCREMENT,
user_type enum('admin','teacher','student') NOT NULL,
username varchar(50) NOT NULL,
email varchar(100) NOT NULL,
password varchar(255) NOT NULL,
PRIMARY KEY (id),
UNIQUE KEY username (username),
UNIQUE KEY email (email)
) ENGINE=InnoDB AUTO_INCREMENT=45 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
