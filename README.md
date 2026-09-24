# Hospital Management System

## 📌 Project Overview

The **Hospital Management System** is a Database Management System (DBMS) project developed using **Oracle SQL**. It is designed to store, organize, and manage important hospital information in a centralized database.

The system manages patient records, doctors, departments, appointments, admissions, treatments, billing, and medicines using relational database concepts.

## 🎯 Objectives

- Maintain patient and doctor records
- Manage hospital departments
- Schedule and track appointments
- Maintain admission and treatment details
- Manage billing and payment information
- Maintain medicine information and stock
- Retrieve information using SQL queries
- Establish relationships between tables using Primary Keys and Foreign Keys

## 🏥 Entities / Tables

The database consists of the following 8 tables:

1. **Patient** – Stores patient personal and contact details.
2. **Doctor** – Stores doctor details and specialization.
3. **Department** – Stores hospital department information.
4. **Appointment** – Stores patient appointment details.
5. **Admission** – Stores patient admission and room details.
6. **Treatment** – Stores diagnosis and treatment information.
7. **Billing** – Stores bill amount and payment status.
8. **Medicine** – Stores medicine name, category, price, and stock.

## 🔑 Database Concepts Used

- Primary Key
- Foreign Key
- NOT NULL Constraint
- UNIQUE Constraint
- CHECK Constraint
- DEFAULT Constraint
- INSERT
- UPDATE
- DELETE
- SELECT
- JOIN
- Relational Database Design
- Normalization

## 🔗 Main Relationships

- Department → Doctor
- Patient → Appointment
- Doctor → Appointment
- Patient → Admission
- Patient → Treatment
- Doctor → Treatment
- Patient → Billing

These relationships are established using Primary Keys and Foreign Keys.

## 💻 Technologies Used

- **Database:** Oracle Database
- **Language:** SQL
- **Tool:** SQL*Plus / Oracle SQL Command Line

## 📂 Project Files

- `hospital_management_system.sql` – Contains the table creation statements, constraints, sample data, and SQL queries.
- `README.md` – Project documentation.

## 📊 Database Operations

The SQL implementation includes:

- Creation of 8 relational tables
- Definition of Primary Keys and Foreign Keys
- Application of database constraints
- Insertion of sample records
- Updating records
- Deleting records
- Retrieving data using SELECT queries
- Joining related tables to retrieve meaningful information

## 👩‍💻 Team Members

- **Y B Sri Lekha** – 25B11AIC90
- **I Mounika Sri** – 25B11AI407
- **P Sahasra** – 25B11AI882
- **P Navya Sri** – 25B11AI932

## 👨‍🏫 Project Guide

**V G L Narasamba**

## 🎓 Department

**Department of Artificial Intelligence & Machine Learning**

**Aditya University**

## 📌 Project Type

**Cornerstone Project – Database Management System**

## 🚀 Future Scope

- Online appointment booking
- Patient portal
- Electronic Medical Records
- Automated billing
- Pharmacy inventory management

## 📄 License

This project is developed for academic and educational purposes.
