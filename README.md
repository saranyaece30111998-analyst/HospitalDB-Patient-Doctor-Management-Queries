# HospitalDB-Patient-Doctor-Management-Queries
Here’s a polished **README.md** you can use directly in your GitHub repository. It’s structured with clear sections, SQL queries, 

---

# 🏥 HospitalDB – SQL Queries & Analysis

This repository contains SQL scripts for managing a **Hospital Database** with three core tables:  
- **Patients**  
- **Doctors**  
- **Appointments**  

It demonstrates **schema design, data insertion, and analytical queries** for real-world hospital management scenarios.

---

## 📌 1. Schema Setup
```sql
CREATE DATABASE HospitalDB;
USE HospitalDB;

-- Patients, Doctors, Appointments table creation with constraints
```
📷 *Screenshot: Database schema setup*

---

## 📌 2. Data Insertion
```sql
-- Insert Patients
-- Insert Doctors
-- Insert Appointments (20 rows)
```
📷 *Screenshot: Inserted records in Patients, Doctors, Appointments*

---

## 📌 3. Basic Queries

### 🔹 Patients in Chennai
```sql
SELECT PatientName, City FROM Patients WHERE City='Chennai';
```
📷 *Screenshot: Patients from Chennai*

---

### 🔹 Patients age above 30
```sql
SELECT PatientName, Age FROM Patients WHERE Age > 30;
```
📷 *Screenshot: Patients older than 30*

---

### 🔹 Male patients in Chennai
```sql
SELECT PatientName, City 
FROM Patients 
WHERE City='Chennai' AND Gender='Male';
```
📷 *Screenshot: Male patients in Chennai*

---

### 🔹 Doctors specialized in Cardiology or Pediatrics
```sql
SELECT DoctorName, Specialization 
FROM HospitalDoctors 
WHERE Specialization IN ('Cardiology','Pediatrics');
```
📷 *Screenshot: Doctors specialization*

---

### 🔹 Patient count by city
```sql
SELECT COUNT(PatientName) AS Patient_Count, City 
FROM Patients 
GROUP BY City;
```
📷 *Screenshot: Patient count grouped by city*

---

## 📌 4. Appointment Queries

### 🔹 Patients with doctor appointments
```sql
SELECT a.AppointmentID, a.PatientID, a.DoctorID, d.DoctorName
FROM Appointments AS a
JOIN HospitalDoctors AS d ON d.DoctorID = a.DoctorID
ORDER BY a.AppointmentID;
```
📷 *Screenshot: Patient appointments with doctors*

---

### 🔹 List all patients and their appointments (if any)
```sql
SELECT a.AppointmentID, a.AppointmentDate, p.PatientID, p.PatientName, a.Status
FROM Patients p
LEFT JOIN Appointments a ON p.PatientID = a.PatientID
ORDER BY a.AppointmentID;
```
📷 *Screenshot: Patients with appointments (including NULLs)*

---

### 🔹 Patients with completed appointments
```sql
SELECT * FROM Patients
WHERE PatientID IN (SELECT PatientID FROM Appointments WHERE Status='Completed');
```
📷 *Screenshot: Patients with completed appointments*

---

## 📌 5. Analytical Queries

### 🔹 Doctors with experience greater than average
```sql
SELECT DoctorID, DoctorName, Experience
FROM HospitalDoctors
WHERE Experience > (SELECT AVG(Experience) FROM HospitalDoctors);
```
📷 *Screenshot: Doctors above average experience*

---

### 🔹 Patients who visited DoctorID = 1
```sql
SELECT p.PatientName, p.PatientID, a.DoctorID
FROM Patients p
JOIN Appointments a ON a.PatientID = p.PatientID
WHERE a.DoctorID = 1;
```
📷 *Screenshot: Patients visiting DoctorID=1*

---

### 🔹 Rank doctors by experience
```sql
SELECT DoctorID, DoctorName, Experience,
       RANK() OVER (ORDER BY Experience DESC) AS ExperienceRank
FROM HospitalDoctors;
```
📷 *Screenshot: Doctor ranking by experience*

---

### 🔹 Patients that visited Dr. Meenakshi
```sql
SELECT p.PatientName, p.PatientID, a.DoctorID, h.DoctorName
FROM Patients p
JOIN Appointments a ON a.PatientID = p.PatientID
JOIN HospitalDoctors h ON h.DoctorID = a.DoctorID
WHERE h.DoctorID = 1;
```
📷 *Screenshot: Patients visiting Dr. Meenakshi*

---

## 📌 6. Key Insights

### 🔹 Patient who booked the most appointments
```sql
SELECT p.PatientID, p.PatientName, COUNT(a.AppointmentID) AS TotalAppointments
FROM Patients p
JOIN Appointments a ON p.PatientID = a.PatientID
GROUP BY p.PatientID, p.PatientName
ORDER BY TotalAppointments DESC
LIMIT 1;
```
📷 *Screenshot: Patient with most appointments*

---

### 🔹 Doctors with 2 or more appointments
```sql
SELECT d.DoctorID, d.DoctorName, COUNT(a.AppointmentID) AS TotalAppointments
FROM HospitalDoctors d
JOIN Appointments a ON d.DoctorID = a.DoctorID
GROUP BY d.DoctorID, d.DoctorName
HAVING COUNT(a.AppointmentID) >= 2
ORDER BY TotalAppointments DESC;
```
📷 *Screenshot: Doctors with 2+ appointments*

---

## ✅ How to Use
1. Clone the repository.  
2. Run the SQL script in **MySQL Workbench / SQL Server / any RDBMS**.  
3. Add screenshots of query outputs in the placeholders above.  

---

✨ This README is structured for **professional GitHub presentation**. Each query has its own section, code block, and screenshot placeholder.  

Would you like me to also add a **Table of Contents with quick links** so readers can jump directly to each query section in GitHub?
