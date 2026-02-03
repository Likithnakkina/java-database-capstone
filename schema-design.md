# Smart Clinic Database Schema Design

This document describes the database schema design for the Smart Clinic Management System. The system uses a combination of MySQL for structured relational data and MongoDB for flexible, document-based data.

---

## MySQL Database Design

MySQL stores structured, relational data that requires validation and relationships.

### Table: patients
- id: INT, Primary Key, Auto Increment
- full_name: VARCHAR(100), Not Null
- email: VARCHAR(100), Unique, Not Null
- password: VARCHAR(255), Not Null
- phone: VARCHAR(15)
- created_at: DATETIME, Not Null

### Table: doctors
- id: INT, Primary Key, Auto Increment
- full_name: VARCHAR(100), Not Null
- specialization: VARCHAR(100), Not Null
- email: VARCHAR(100), Unique, Not Null
- phone: VARCHAR(15)
- available: BOOLEAN, Default true

### Table: appointments
- id: INT, Primary Key, Auto Increment
- patient_id: INT, Foreign Key → patients(id)
- doctor_id: INT, Foreign Key → doctors(id)
- appointment_time: DATETIME, Not Null
- duration_minutes: INT, Default 60
- status: INT (0 = Scheduled, 1 = Completed, 2 = Cancelled)

### Table: admin
- id: INT, Primary Key, Auto Increment
- username: VARCHAR(50), Unique, Not Null
- password: VARCHAR(255), Not Null
- role: VARCHAR(20), Default 'ADMIN'

#### Notes:
- Appointments are linked to patients and doctors.
- If a patient or doctor is deleted, related appointments should be handled carefully.
- Doctors cannot have overlapping appointments (enforced at service level).
- Patient appointment history is retained for auditing and reference.

---

## MongoDB Collection Design

MongoDB stores flexible data like prescriptions, feedback, and logs.

### Collection: prescriptions
```json
{
  "_id": "ObjectId('64abc123456')",
  "appointmentId": 102,
  "patientId": 15,
  "doctorId": 7,
  "medications": [
    {
      "name": "Paracetamol",
      "dosage": "500mg",
      "frequency": "Twice a day"
    }
  ],
  "doctorNotes": "Take medicine after meals and drink plenty of water.",
  "refillCount": 1,
  "createdAt": "2026-02-01T10:30:00Z",
  "tags": ["fever", "pain-relief"]
}
