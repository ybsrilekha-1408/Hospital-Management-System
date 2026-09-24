-- =========================================================
-- HOSPITAL MANAGEMENT SYSTEM
-- Oracle SQL Project
-- =========================================================

-- =========================================================
-- 1. CREATE TABLES
-- =========================================================

-- DEPARTMENT TABLE
CREATE TABLE Department (
    Department_ID NUMBER PRIMARY KEY,
    Department_Name VARCHAR2(50) NOT NULL UNIQUE,
    Location VARCHAR2(100) NOT NULL,
    Contact_No VARCHAR2(15) UNIQUE
);

-- PATIENT TABLE
CREATE TABLE Patient (
    Patient_ID NUMBER PRIMARY KEY,
    First_Name VARCHAR2(50) NOT NULL,
    Last_Name VARCHAR2(50) NOT NULL,
    Gender VARCHAR2(10) NOT NULL
        CHECK (Gender IN ('Male', 'Female', 'Other')),
    Date_of_Birth DATE NOT NULL,
    Phone VARCHAR2(15) UNIQUE,
    Address VARCHAR2(150) NOT NULL
);

-- DOCTOR TABLE
CREATE TABLE Doctor (
    Doctor_ID NUMBER PRIMARY KEY,
    Doctor_Name VARCHAR2(100) NOT NULL,
    Specialization VARCHAR2(50) NOT NULL,
    Phone VARCHAR2(15) UNIQUE,
    Email VARCHAR2(100) UNIQUE,
    Department_ID NUMBER NOT NULL,
    FOREIGN KEY (Department_ID)
        REFERENCES Department(Department_ID)
);

-- APPOINTMENT TABLE
CREATE TABLE Appointment (
    Appointment_ID NUMBER PRIMARY KEY,
    Patient_ID NUMBER NOT NULL,
    Doctor_ID NUMBER NOT NULL,
    Appointment_Date DATE NOT NULL,
    Appointment_Time VARCHAR2(10) NOT NULL,
    Status VARCHAR2(20) DEFAULT 'Scheduled',
    FOREIGN KEY (Patient_ID)
        REFERENCES Patient(Patient_ID),
    FOREIGN KEY (Doctor_ID)
        REFERENCES Doctor(Doctor_ID)
);

-- ADMISSION TABLE
CREATE TABLE Admission (
    Admission_ID NUMBER PRIMARY KEY,
    Patient_ID NUMBER NOT NULL,
    Room_ID NUMBER NOT NULL,
    Admission_Date DATE NOT NULL,
    Discharge_Date DATE,
    FOREIGN KEY (Patient_ID)
        REFERENCES Patient(Patient_ID),
    CHECK (Discharge_Date IS NULL OR Discharge_Date >= Admission_Date)
);

-- TREATMENT TABLE
CREATE TABLE Treatment (
    Treatment_ID NUMBER PRIMARY KEY,
    Patient_ID NUMBER NOT NULL,
    Doctor_ID NUMBER NOT NULL,
    Diagnosis VARCHAR2(200) NOT NULL,
    FOREIGN KEY (Patient_ID)
        REFERENCES Patient(Patient_ID),
    FOREIGN KEY (Doctor_ID)
        REFERENCES Doctor(Doctor_ID)
);

-- BILLING TABLE
CREATE TABLE Billing (
    Bill_ID NUMBER PRIMARY KEY,
    Patient_ID NUMBER NOT NULL,
    Amount NUMBER(10,2) NOT NULL
        CHECK (Amount >= 0),
    Payment_Status VARCHAR2(20) DEFAULT 'Pending',
    FOREIGN KEY (Patient_ID)
        REFERENCES Patient(Patient_ID)
);

-- MEDICINE TABLE
CREATE TABLE Medicine (
    Medicine_ID NUMBER PRIMARY KEY,
    Name VARCHAR2(100) NOT NULL UNIQUE,
    Category VARCHAR2(50) NOT NULL,
    Price NUMBER(10,2) NOT NULL
        CHECK (Price >= 0),
    Stock NUMBER DEFAULT 0
        CHECK (Stock >= 0)
);


-- =========================================================
-- 2. INSERT SAMPLE DATA
-- =========================================================

-- DEPARTMENT DATA

INSERT INTO Department
VALUES (1, 'Cardiology', 'Block A', '9876543210');

INSERT INTO Department
VALUES (2, 'Neurology', 'Block B', '9876543211');

INSERT INTO Department
VALUES (3, 'Orthopedics', 'Block C', '9876543212');

INSERT INTO Department
VALUES (4, 'Pediatrics', 'Block D', '9876543213');

INSERT INTO Department
VALUES (5, 'General Medicine', 'Block E', '9876543214');


-- PATIENT DATA

INSERT INTO Patient
VALUES (101, 'Rahul', 'Kumar', 'Male',
        DATE '2000-05-12', '9876500001', 'Hyderabad');

INSERT INTO Patient
VALUES (102, 'Ananya', 'Rao', 'Female',
        DATE '1999-08-20', '9876500002', 'Hyderabad');

INSERT INTO Patient
VALUES (103, 'Arjun', 'Reddy', 'Male',
        DATE '2001-02-15', '9876500003', 'Vijayawada');

INSERT INTO Patient
VALUES (104, 'Sneha', 'Sharma', 'Female',
        DATE '2002-11-10', '9876500004', 'Visakhapatnam');

INSERT INTO Patient
VALUES (105, 'Kiran', 'Kumar', 'Male',
        DATE '1998-06-25', '9876500005', 'Kakinada');


-- DOCTOR DATA

INSERT INTO Doctor
VALUES (201, 'Dr. Suresh', 'Cardiologist',
        '9876510001', 'suresh@hospital.com', 1);

INSERT INTO Doctor
VALUES (202, 'Dr. Priya', 'Neurologist',
        '9876510002', 'priya@hospital.com', 2);

INSERT INTO Doctor
VALUES (203, 'Dr. Ramesh', 'Orthopedic',
        '9876510003', 'ramesh@hospital.com', 3);

INSERT INTO Doctor
VALUES (204, 'Dr. Kavya', 'Pediatrician',
        '9876510004', 'kavya@hospital.com', 4);

INSERT INTO Doctor
VALUES (205, 'Dr. Arun', 'General Physician',
        '9876510005', 'arun@hospital.com', 5);


-- APPOINTMENT DATA

INSERT INTO Appointment
VALUES (301, 101, 201, DATE '2026-09-25', '10:00 AM', 'Scheduled');

INSERT INTO Appointment
VALUES (302, 102, 202, DATE '2026-09-25', '11:00 AM', 'Scheduled');

INSERT INTO Appointment
VALUES (303, 103, 203, DATE '2026-09-26', '09:30 AM', 'Scheduled');

INSERT INTO Appointment
VALUES (304, 104, 204, DATE '2026-09-26', '12:00 PM', 'Completed');

INSERT INTO Appointment
VALUES (305, 105, 205, DATE '2026-09-27', '10:30 AM', 'Scheduled');


-- ADMISSION DATA

INSERT INTO Admission
VALUES (401, 101, 101, DATE '2026-09-20', DATE '2026-09-23');

INSERT INTO Admission
VALUES (402, 102, 102, DATE '2026-09-21', DATE '2026-09-24');

INSERT INTO Admission
VALUES (403, 103, 103, DATE '2026-09-22', NULL);

INSERT INTO Admission
VALUES (404, 104, 104, DATE '2026-09-23', NULL);

INSERT INTO Admission
VALUES (405, 105, 105, DATE '2026-09-24', NULL);


-- TREATMENT DATA

INSERT INTO Treatment
VALUES (501, 101, 201, 'Chest Pain and Heart Checkup');

INSERT INTO Treatment
VALUES (502, 102, 202, 'Migraine Treatment');

INSERT INTO Treatment
VALUES (503, 103, 203, 'Knee Pain Treatment');

INSERT INTO Treatment
VALUES (504, 104, 204, 'Fever and Cold');

INSERT INTO Treatment
VALUES (505, 105, 205, 'General Health Checkup');


-- BILLING DATA

INSERT INTO Billing
VALUES (601, 101, 15000, 'Paid');

INSERT INTO Billing
VALUES (602, 102, 8500, 'Paid');

INSERT INTO Billing
VALUES (603, 103, 12000, 'Pending');

INSERT INTO Billing
VALUES (604, 104, 6500, 'Paid');

INSERT INTO Billing
VALUES (605, 105, 5000, 'Pending');


-- MEDICINE DATA

INSERT INTO Medicine
VALUES (701, 'Paracetamol', 'Tablet', 20, 100);

INSERT INTO Medicine
VALUES (702, 'Amoxicillin', 'Antibiotic', 50, 80);

INSERT INTO Medicine
VALUES (703, 'Ibuprofen', 'Tablet', 30, 75);

INSERT INTO Medicine
VALUES (704, 'Cetirizine', 'Tablet', 15, 120);

INSERT INTO Medicine
VALUES (705, 'Azithromycin', 'Antibiotic', 60, 50);

COMMIT;


-- =========================================================
-- 3. UPDATE OPERATION
-- =========================================================

UPDATE Patient
SET Address = 'Hyderabad'
WHERE Patient_ID = 101;

COMMIT;


-- =========================================================
-- 4. DELETE OPERATION
-- =========================================================

DELETE FROM Appointment
WHERE Appointment_ID = 305;

COMMIT;


-- =========================================================
-- 5. SAMPLE SQL QUERIES
-- =========================================================

-- Display all patients
SELECT * FROM Patient;


-- Display doctors with their departments
SELECT
    d.Doctor_ID,
    d.Doctor_Name,
    d.Specialization,
    dp.Department_Name
FROM Doctor d
JOIN Department dp
ON d.Department_ID = dp.Department_ID;


-- Display appointments with patient and doctor details
SELECT
    p.First_Name,
    p.Last_Name,
    d.Doctor_Name,
    a.Appointment_Date,
    a.Appointment_Time,
    a.Status
FROM Appointment a
JOIN Patient p
ON a.Patient_ID = p.Patient_ID
JOIN Doctor d
ON a.Doctor_ID = d.Doctor_ID;


-- Display patient billing details
SELECT
    p.Patient_ID,
    p.First_Name,
    p.Last_Name,
    b.Amount,
    b.Payment_Status
FROM Patient p
JOIN Billing b
ON p.Patient_ID = b.Patient_ID;


-- Display treatment details
SELECT
    p.First_Name,
    p.Last_Name,
    d.Doctor_Name,
    t.Diagnosis
FROM Treatment t
JOIN Patient p
ON t.Patient_ID = p.Patient_ID
JOIN Doctor d
ON t.Doctor_ID = d.Doctor_ID;


-- Display medicines with price and stock
SELECT
    Name,
    Category,
    Price,
    Stock
FROM Medicine;