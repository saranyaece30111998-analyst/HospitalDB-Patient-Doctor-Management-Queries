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
---

## 📌 2. Data Insertion
```sql
-- Insert Patients
-- Insert Doctors
-- Insert Appointments (20 rows)
```

- <img width="970" height="887" alt="Screenshot 2026-06-16 170438" src="https://github.com/user-attachments/assets/eac3dbab-8bd5-4769-ad53-e18826e0398d" />

---

## 📌 3. Basic Queries

### 🔹 Patients in Chennai
```sql
SELECT PatientName, City FROM Patients WHERE City='Chennai';
```
- <img width="527" height="357" alt="Screenshot 2026-06-14 201013" src="https://github.com/user-attachments/assets/d179de06-f87b-4231-94e3-a887bc0645a5" />


---

### 🔹 Patients age above 30
```sql
SELECT PatientName, Age FROM Patients WHERE Age > 30;
```
- <img width="532" height="421" alt="Screenshot 2026-06-15 133404" src="https://github.com/user-attachments/assets/b7eaf7b9-6ddc-4701-9291-27aa69a7b4d5" />


---

### 🔹 Male patients in Chennai
```sql
SELECT PatientName, City 
FROM Patients 
WHERE City='Chennai' AND Gender='Male';
```
- <img width="572" height="407" alt="Screenshot 2026-06-15 133534" src="https://github.com/user-attachments/assets/48e9af7c-3c3b-4284-bea1-30e17796878e" />


---

### 🔹 Doctors specialized in Cardiology or Pediatrics
```sql
SELECT DoctorName, Specialization 
FROM HospitalDoctors 
WHERE Specialization IN ('Cardiology','Pediatrics');
```
- <img width="777" height="475" alt="Screenshot 2026-06-15 133947" src="https://github.com/user-attachments/assets/f70abfea-77b5-4c3c-bfd2-aa8be7d904cb" />


---

### 🔹 Patient count by city
```sql
SELECT COUNT(PatientName) AS Patient_Count, City 
FROM Patients 
GROUP BY City;
```
- <img width="516" height="381" alt="Screenshot 2026-06-15 134033" src="https://github.com/user-attachments/assets/b0d71bb3-93b2-45fc-9156-84cdc58d1fd2" />


---

## 📌 4. Appointment Queries

### 🔹 Patients with doctor appointments
```sql
SELECT a.AppointmentID, a.PatientID, a.DoctorID, d.DoctorName
FROM Appointments AS a
JOIN HospitalDoctors AS d ON d.DoctorID = a.DoctorID
ORDER BY a.AppointmentID;
```
- <img width="622" height="607" alt="Screenshot 2026-06-15 134738" src="https://github.com/user-attachments/assets/3a8f55a2-22ac-469e-8b97-91a301a506ac" />

---

### 🔹 List all patients and their appointments (if any)
```sql
SELECT a.AppointmentID, a.AppointmentDate, p.PatientID, p.PatientName, a.Status
FROM Patients p
LEFT JOIN Appointments a ON p.PatientID = a.PatientID
ORDER BY a.AppointmentID;
```
- <img width="696" height="607" alt="Screenshot 2026-06-15 135233" src="https://github.com/user-attachments/assets/aa7dd543-96a6-47ff-8f8f-f57846ee0cfe" />



---

### 🔹 Patients with completed appointments
```sql
SELECT * FROM Patients
WHERE PatientID IN (SELECT PatientID FROM Appointments WHERE Status='Completed');
```
- <img width="696" height="607" alt="Screenshot 2026-06-15 135233" src="https://github.com/user-attachments/assets/40174c54-59ec-434b-bbec-99be8064b71d" />


---

## 📌 5. Analytical Queries

### 🔹 Doctors with experience greater than average
```sql
SELECT DoctorID, DoctorName, Experience
FROM HospitalDoctors
WHERE Experience > (SELECT AVG(Experience) FROM HospitalDoctors);
```
- <img width="737" height="530" alt="Screenshot 2026-06-15 135303" src="https://github.com/user-attachments/assets/51e1664d-8c02-4ea7-96b9-19f044d25756" />


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
