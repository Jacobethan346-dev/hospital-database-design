# Hospital database entity relationships

Reconstructed from the foreign-key fields in the original diagram. Mandatory relationships are working assumptions; an appointment may have no assigned room.

```mermaid
erDiagram
    DEPARTMENT ||--o{ DOCTOR : employs
    DEPARTMENT ||--o{ NURSE : employs
    DEPARTMENT ||--o{ ROOM : contains
    PATIENT ||--o{ APPOINTMENT : schedules
    DOCTOR ||--o{ APPOINTMENT : attends
    ROOM |o--o{ APPOINTMENT : hosts
    PATIENT ||--o{ TREATMENT : receives
    DOCTOR ||--o{ TREATMENT : provides
    PATIENT ||--o{ MEDICAL_RECORD : has
    PATIENT {
        int PatientID PK
        varchar FirstName
        varchar LastName
        date DateOfBirth
        char Gender
        varchar Address
        varchar Phone
        varchar BloodType
        varchar InsuranceNumber
    }
    DOCTOR {
        int DoctorID PK
        varchar FirstName
        varchar LastName
        varchar Specialization
        varchar LicenseNumber
        varchar Phone
        int DepartmentID FK
        int YearsOfExperience
    }
    NURSE {
        int NurseID PK
        varchar FirstName
        varchar LastName
        varchar LicenseNumber
        varchar Phone
        int DepartmentID FK
        varchar Shift
    }
    DEPARTMENT {
        int DepartmentID PK
        varchar DepartmentName
        varchar Location
        varchar Phone
        decimal Budget
    }
    APPOINTMENT {
        int AppointmentID PK
        int PatientID FK
        int DoctorID FK
        datetime AppointmentDate
        text Reason
        varchar Status
        int RoomID FK
    }
    TREATMENT {
        int TreatmentID PK
        int PatientID FK
        int DoctorID FK
        varchar TreatmentType
        date TreatmentDate
        text Description
        decimal Cost
    }
    ROOM {
        int RoomID PK
        varchar RoomNumber
        varchar RoomType
        int Floor
        int DepartmentID FK
        boolean Available
    }
    MEDICAL_RECORD {
        int RecordID PK
        int PatientID FK
        text Diagnosis
        text Allergies
        text Medications
        date RecordDate
    }
```
