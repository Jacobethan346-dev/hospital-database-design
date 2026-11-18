# Hospital design notes

## Recovered source

The source is hospital_er_diagram.drawio. A second saved drawing contains the same eight entity definitions. The original assignment is represented here as a database design, without an invented claim that SQL, sample data, or a production app was part of the submission.

## Relationship interpretation

PatientID connects APPOINTMENT, TREATMENT, and MEDICAL_RECORD to PATIENT. DoctorID connects appointments and treatments to DOCTOR. DepartmentID connects doctors, nurses, and rooms to DEPARTMENT. RoomID connects appointments to ROOM.

The Mermaid reconstruction restores relationships implied by those fields, including the incomplete doctor/appointment connector. Its one-to-many cardinalities assume each appointment has one patient and doctor, each treatment has one patient and doctor, and each staff member/room belongs to one department. Optionality was not fully specified in the source; appointment room assignment is shown as optional.

## Decisions needed for implementation

- Define VARCHAR lengths, currency precision, nullability, and permitted status values.
- Choose uniqueness rules for room and professional license numbers.
- Represent allergies and medications as related records when multiple values must be queried individually.
- Define appointment duration and overlap handling for doctors and rooms.
- Clarify whether a treatment links to an appointment or can occur independently.
- Decide whether historical department membership and room allocation must be preserved.
- Clarify entity identification: MEDICAL_RECORD has its own RecordID, which is inconsistent with treating it as an identifying weak entity solely because it belongs to a patient.
- Define access controls and auditing if the design is ever developed beyond a classroom model.

## Portfolio changes

Added documentation and a readable diagram based on the source entity fields. No patient dataset was added. The original .drawio model remains available for comparison and editing.
