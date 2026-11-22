sql-- ==========================================
## MySQL Assignment 1 – DDL Commands & Constraints ## 
-- Database: employee
-- ==========================================

## 1. CREATE DATABASE & TABLES
CREATE DATABASE employee;
USE employee;

CREATE TABLE Departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL UNIQUE,
    department_head VARCHAR(100));

CREATE TABLE Location (
    location_id INT PRIMARY KEY AUTO_INCREMENT,
    location_name VARCHAR(100) NOT NULL UNIQUE,
    city VARCHAR(100));

CREATE TABLE Employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100) NOT NULL,
    age INT,
    gender CHAR(1),
    designation VARCHAR(50),
    hire_date DATE,
    department_id INT,
    location_id INT);

## 2. ALTER TABLE
ALTER TABLE Employees ADD COLUMN email VARCHAR(100);
ALTER TABLE Employees MODIFY COLUMN designation VARCHAR(100);
ALTER TABLE Employees DROP COLUMN age;
ALTER TABLE Employees RENAME COLUMN hire_date TO date_of_joining;

## 3. RENAME TABLES
RENAME TABLE Departments TO Departments_Info;
RENAME TABLE Location TO Locations;

## 4. TRUNCATE TABLE
TRUNCATE TABLE Employees;

## 5. DROP TABLE & DATABASE
DROP TABLE Employees;
DROP DATABASE employee;

-- ==========================================
## CONSTRAINTS PART - RECREATE WITH CONSTRAINTS
-- ==========================================

CREATE DATABASE IF NOT EXISTS employee;
USE employee;

## Departments: department_id PK, department_name UNIQUE + NOT NULL
CREATE TABLE Departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL UNIQUE);

## Location: AUTO_INCREMENT, UNIQUE + NOT NULL
CREATE TABLE Location (
    location_id INT PRIMARY KEY AUTO_INCREMENT,
    location_name VARCHAR(100) NOT NULL UNIQUE);

## Employees: All Constraints
CREATE TABLE Employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100) NOT NULL,
    gender CHAR(1) CHECK (gender IN ('M', 'F')),
    age INT CHECK (age >= 18),
    designation VARCHAR(100),
    email VARCHAR(100),
    hire_date DATE DEFAULT (CURRENT_DATE),
    department_id INT,
    location_id INT,
    FOREIGN KEY (department_id) REFERENCES Departments(department_id),
    FOREIGN KEY (location_id) REFERENCES Location(location_id));
