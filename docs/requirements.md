# Requirements — Smart Clinic Appointment & Patient Portal

## 1. Document Information

- **Project:** Smart Clinic Appointment & Patient Portal
- **Artifact:** Requirements + Business Rules
- **Document:** `docs/02-requirements/requirements.md`
- **Status:** Draft for review
- **Version:** 0.1
- **Last Updated:** 2026-08-26

---

# 2. Problem Context

## 2.1 Business Problem

The clinic needs a system to organize doctor schedules, patient appointments, check-in, and consultation queues in a consistent workflow.

The system should support the following mandatory workflow:

```text
Search Doctor
    ↓
Book
    ↓
Confirm
    ↓
Check-in
    ↓
Consult
    ↓
Follow-up
```

## 2.2 Primary Roles

The system must support at least the following roles:

- **Patient**
- **Doctor**
- **Receptionist**
- **Admin**

## 2.3 AI Feature

The system may provide AI-assisted recommendations for doctors and appointment schedules based on the patient's stated needs and constraints.

The AI feature is **not intended for diagnosis or treatment decisions**.

---

# 3. Requirement Classification

This document uses the following requirement types:

| Type | Meaning |
|---|---|
| FR | Functional Requirement |
| NFR | Non-functional Requirement |
| BR | Business Rule |
| CON | Constraint |
| ASM | Assumption |
| Q | Open Question |

Priority:

| Priority | Meaning |
|---|---|
| Must | Required for MVP |
| Should | Important but not critical for MVP |
| Could | Optional if time/resources permit |

---

# 4. Scope

## 4.1 In Scope — Must

The MVP must support:

1. Doctor search.
2. Doctor schedule availability.
3. Appointment booking.
4. Appointment confirmation.
5. Patient check-in.
6. Queue management.
7. Doctor consultation workflow.
8. Follow-up information.
9. Appointment-related notifications.
10. AI-assisted doctor/schedule recommendations based on stated needs and constraints.

## 4.2 In Scope — Should

The following items are currently considered candidates for the next scope level:

1. Additional doctor filtering options.
2. Additional appointment management capabilities.
3. Extended appointment history.
4. Additional notification preferences.

These items require confirmation before being treated as confirmed requirements.

## 4.3 In Scope — Could

Potential future capabilities:

1. More advanced AI recommendation behavior.
2. Personalized recommendation based on historical preferences.
3. Additional convenience features around scheduling and notifications.

These items are not required for the MVP.

## 4.4 Out of Scope

The following are outside the current project scope:

1. Medical diagnosis by AI.
2. AI-generated treatment decisions.
3. AI replacing a doctor's clinical judgment.
4. Other medical functions not explicitly defined in the project scope.

---

# 5. Functional Requirements

## REQ-001 — Search Doctors

- **Type:** FR
- **Source:** Project brief / group definition
- **Priority:** Must
- **Statement:** Patient can search for doctors available through the clinic.
- **Rationale:** Doctor search is the first mandatory step of the appointment workflow.
- **Acceptance signal:** A patient can submit a search request and receive matching doctors.
- **Dependencies:** Doctor
- **Status:** Confirmed

### Acceptance Criteria

#### AC-001-01

- **Given:** The system contains available doctors.
- **When:** A patient searches for a doctor.
- **Then:** The system displays doctors matching the search criteria.

#### AC-001-02

- **Given:** No doctor matches the search criteria.
- **When:** The patient submits the search.
- **Then:** The system displays an empty-result state.

---

## REQ-002 — View Doctor Schedule

- **Type:** FR
- **Source:** Project brief / group definition
- **Priority:** Must
- **Statement:** Patient can view available appointment schedules for a selected doctor.
- **Rationale:** Patients need to identify an available appointment slot before booking.
- **Acceptance signal:** A selected doctor displays available schedule information.
- **Dependencies:** Doctor, Schedule
- **Status:** Confirmed

### Acceptance Criteria

#### AC-002-01

- **Given:** A doctor has available appointment slots.
- **When:** The patient selects the doctor.
- **Then:** The system displays the available slots.

#### AC-002-02

- **Given:** A doctor has no available slots for the selected period.
- **When:** The patient views the doctor's schedule.
- **Then:** The system indicates that no available slots exist for that period.

---

## REQ-003 — Filter Doctor or Schedule Results

- **Type:** FR
- **Source:** Project brief / group definition
- **Priority:** Should
- **Statement:** Patient can filter doctor or schedule results according to available scheduling criteria such as date or time.
- **Rationale:** Filtering can help patients find a suitable appointment more efficiently.
- **Acceptance signal:** Applying a filter changes the displayed result set according to the selected criteria.
- **Dependencies:** Doctor, Schedule
- **Status:** Draft

---

## REQ-004 — Book Appointment

- **Type:** FR
- **Source:** Mandatory workflow
- **Priority:** Must
- **Statement:** Patient can book an available appointment slot.
- **Rationale:** Booking is a core function of the clinic appointment workflow.
- **Acceptance signal:** A valid booking request creates an appointment associated with the patient, doctor, and selected schedule.
- **Dependencies:** Patient, Doctor, Schedule
- **Status:** Confirmed

### Acceptance Criteria

#### AC-004-01

- **Given:** The selected appointment slot is available.
- **When:** The patient submits a booking request.
- **Then:** The system creates an appointment for the selected patient, doctor, and schedule.

#### AC-004-02

- **Given:** The selected appointment slot is no longer available.
- **When:** The patient submits a booking request.
- **Then:** The system rejects the booking and informs the patient that the slot is unavailable.

---

## REQ-005 — Review Appointment Details Before Confirmation

- **Type:** FR
- **Source:** Mandatory workflow
- **Priority:** Must
- **Statement:** Patient can review appointment information before confirming the appointment.
- **Rationale:** The patient should be able to verify the selected doctor, schedule, and appointment information before confirmation.
- **Acceptance signal:** A review state displays the relevant appointment information before confirmation.
- **Dependencies:** Appointment, Doctor, Schedule
- **Status:** Confirmed

---

## REQ-006 — Confirm Appointment

- **Type:** FR
- **Source:** Mandatory workflow
- **Priority:** Must
- **Statement:** Patient can confirm a valid booked appointment.
- **Rationale:** Confirmation is a mandatory step before check-in.
- **Acceptance signal:** A confirmed appointment transitions to the appropriate confirmed state.
- **Dependencies:** Appointment
- **Status:** Confirmed

### Acceptance Criteria

#### AC-006-01

- **Given:** A valid appointment exists and is eligible for confirmation.
- **When:** The patient confirms the appointment.
- **Then:** The system marks the appointment as confirmed.

#### AC-006-02

- **Given:** The appointment is not eligible for confirmation.
- **When:** The patient attempts to confirm it.
- **Then:** The system rejects the action and displays an appropriate message.

---

## REQ-007 — Patient Check-in

- **Type:** FR
- **Source:** Mandatory workflow
- **Priority:** Must
- **Statement:** Receptionist can check in a patient with an eligible confirmed appointment.
- **Rationale:** Check-in initiates the queue management stage of the clinic workflow.
- **Acceptance signal:** A successful check-in creates or updates the patient's queue entry.
- **Dependencies:** Patient, Appointment, Queue, Receptionist
- **Status:** Confirmed

---

## REQ-008 — Assign Queue Position

- **Type:** FR
- **Source:** Mandatory workflow / domain object definition
- **Priority:** Must
- **Statement:** The system can assign a queue position to a successfully checked-in patient.
- **Rationale:** Queue organization is part of the core business problem.
- **Acceptance signal:** A checked-in patient receives a queue position associated with the relevant consultation session.
- **Dependencies:** Queue, Appointment, Visit
- **Status:** Confirmed

---

## REQ-009 — View Consultation Queue

- **Type:** FR
- **Source:** Mandatory workflow
- **Priority:** Must
- **Statement:** Doctor can view the current consultation queue.
- **Rationale:** Doctors need queue visibility to manage patient consultations.
- **Acceptance signal:** The doctor can view patients currently waiting in the relevant queue.
- **Dependencies:** Queue, Doctor
- **Status:** Confirmed

---

## REQ-010 — Record Consultation Visit

- **Type:** FR
- **Source:** Mandatory workflow / domain object definition
- **Priority:** Must
- **Statement:** Doctor can record consultation information for a visit.
- **Rationale:** The consultation stage must produce a visit record.
- **Acceptance signal:** A doctor can save consultation information associated with the appropriate visit.
- **Dependencies:** Doctor, Patient, Visit, Appointment
- **Status:** Confirmed

---

## REQ-011 — Follow-up Information

- **Type:** FR
- **Source:** Mandatory workflow
- **Priority:** Must
- **Statement:** Doctor can record follow-up information associated with a visit, and the patient can view the resulting follow-up information.
- **Rationale:** Follow-up is the final mandatory stage of the project workflow.
- **Acceptance signal:** Follow-up information is stored and available to the relevant patient.
- **Dependencies:** Doctor, Patient, Visit
- **Status:** Confirmed

---

## REQ-012 — Appointment Notifications

- **Type:** FR
- **Source:** Domain object definition
- **Priority:** Must
- **Statement:** System can send appointment-related notifications to patients.
- **Rationale:** Notifications support communication around appointment-related events.
- **Acceptance signal:** A defined appointment event results in the corresponding notification being created or delivered.
- **Dependencies:** Appointment, Notification
- **Status:** Confirmed

---

## REQ-013 — AI-assisted Doctor Recommendation

- **Type:** FR
- **Source:** Proposed AI feature
- **Priority:** Should
- **Statement:** Patient can request AI-assisted recommendations for doctors based on stated needs and constraints.
- **Rationale:** AI assistance can reduce the effort required to identify suitable doctors.
- **Acceptance signal:** The system returns recommendation results based on the provided needs and constraints.
- **Dependencies:** Doctor, AI feature
- **Status:** Confirmed

### Acceptance Criteria

#### AC-013-01

- **Given:** The patient provides a valid need and applicable constraints.
- **When:** The patient requests an AI-assisted doctor recommendation.
- **Then:** The system returns one or more suitable doctor recommendations based on the available information.

#### AC-013-02

- **Given:** The provided information is insufficient to make a meaningful recommendation.
- **When:** The patient requests a recommendation.
- **Then:** The system asks for additional information or indicates that there is insufficient information.

---

## REQ-014 — AI-assisted Schedule Recommendation

- **Type:** FR
- **Source:** Proposed AI feature
- **Priority:** Should
- **Statement:** Patient can request AI-assisted recommendations for appointment schedules based on stated needs and scheduling constraints.
- **Rationale:** AI assistance can help patients identify suitable available schedules more efficiently.
- **Acceptance signal:** The system returns available schedule recommendations that satisfy the provided constraints where possible.
- **Dependencies:** Schedule, Appointment, AI feature
- **Status:** Confirmed

### Acceptance Criteria

#### AC-014-01

- **Given:** Available schedules exist that satisfy the patient's stated constraints.
- **When:** The patient requests an AI-assisted schedule recommendation.
- **Then:** The system returns matching available schedules.

#### AC-014-02

- **Given:** No available schedule satisfies the stated constraints.
- **When:** The patient requests a recommendation.
- **Then:** The system indicates that no matching schedule is available.

---

# 6. Non-functional Requirements

> Note: The following NFRs are included as initial project requirements. Exact target values that were not defined in the current project brief should be reviewed by the group before being treated as final.

## NFR-001 — Authentication and Role-based Access

- **Type:** NFR
- **Source:** Minimum role definition
- **Priority:** Must
- **Statement:** Access to role-specific functions must be restricted according to the authenticated user's role.
- **Rationale:** Patient, Doctor, Receptionist, and Admin have different responsibilities.
- **Acceptance signal:** Unauthorized role-based access attempts are rejected.
- **Dependencies:** Authentication, roles
- **Status:** Draft

---

## NFR-002 — Data Integrity

- **Type:** NFR
- **Source:** Core appointment workflow
- **Priority:** Must
- **Statement:** The system must maintain consistent appointment and schedule data and must not allow conflicting bookings for the same unavailable slot.
- **Rationale:** Appointment conflicts directly affect the clinic's scheduling process.
- **Acceptance signal:** Concurrent or repeated booking attempts cannot produce conflicting confirmed appointments for the same unavailable slot.
- **Dependencies:** Appointment, Schedule
- **Status:** Draft

---

## NFR-003 — Usability

- **Type:** NFR
- **Source:** Patient-facing workflow
- **Priority:** Should
- **Statement:** The patient-facing appointment workflow should provide clear feedback for successful, invalid, unavailable, and error states.
- **Rationale:** Patients need to understand the current state of their booking.
- **Acceptance signal:** Main workflow states display clear status and actionable feedback.
- **Dependencies:** UI/UX design
- **Status:** Draft

---

## NFR-004 — Performance

- **Type:** NFR
- **Source:** Project quality requirement
- **Priority:** Should
- **Statement:** Core search and appointment interactions should provide acceptable response time under the project's expected demo conditions.
- **Rationale:** Slow interaction can negatively affect appointment management.
- **Acceptance signal:** Performance is measured during testing and compared against a target agreed by the group.
- **Dependencies:** Infrastructure, API
- **Status:** Draft

**Open point:** Exact response-time target is not yet defined.

---

## NFR-005 — Availability of Critical Data

- **Type:** NFR
- **Source:** Clinic workflow
- **Priority:** Must
- **Statement:** Appointment, schedule, and queue information required for critical workflow steps must be available to authorized users when the corresponding operation is performed.
- **Rationale:** Missing or stale operational information can disrupt appointment and queue management.
- **Acceptance signal:** Critical workflow operations can retrieve the required authoritative data.
- **Dependencies:** Database, API
- **Status:** Draft

---

# 7. Business Rules

## BR-001 — Only Available Slots Can Be Booked

- **Type:** BR
- **Source:** Core appointment workflow
- **Priority:** Must
- **Statement:** An appointment can only be booked when the selected schedule slot is available.
- **Related Requirements:** REQ-004, NFR-002
- **Status:** Confirmed

---

## BR-002 — A Slot Cannot Be Double-booked

- **Type:** BR
- **Source:** Appointment domain
- **Priority:** Must
- **Statement:** A single appointment slot cannot be assigned to conflicting appointments.
- **Related Requirements:** REQ-004, NFR-002
- **Status:** Confirmed

---

## BR-003 — Confirmation Is Required Before Check-in

- **Type:** BR
- **Source:** Mandatory workflow
- **Priority:** Must
- **Statement:** A patient must have a confirmed appointment before the appointment can proceed to check-in.
- **Related Requirements:** REQ-006, REQ-007
- **Status:** Confirmed

---

## BR-004 — Queue Entry Follows Successful Check-in

- **Type:** BR
- **Source:** Mandatory workflow
- **Priority:** Must
- **Statement:** A patient receives a queue entry only after a valid check-in.
- **Related Requirements:** REQ-007, REQ-008
- **Status:** Confirmed

---

## BR-005 — Consultation Is Associated With a Visit

- **Type:** BR
- **Source:** Domain model
- **Priority:** Must
- **Statement:** Consultation information must be associated with the appropriate visit record.
- **Related Requirements:** REQ-010
- **Status:** Confirmed

---

## BR-006 — Follow-up Is Associated With the Visit

- **Type:** BR
- **Source:** Mandatory workflow
- **Priority:** Must
- **Statement:** Follow-up information must be associated with the corresponding consultation visit.
- **Related Requirements:** REQ-011
- **Status:** Confirmed

---

## BR-007 — AI Must Not Diagnose

- **Type:** BR
- **Source:** Proposed AI feature
- **Priority:** Must
- **Statement:** The AI feature must not provide medical diagnosis or replace clinical judgment.
- **Related Requirements:** REQ-013, REQ-014
- **Status:** Confirmed

---

## BR-008 — AI Recommendation Must Respect User Constraints

- **Type:** BR
- **Source:** Proposed AI feature
- **Priority:** Must
- **Statement:** AI recommendations should be generated using the patient's explicitly provided needs and scheduling constraints.
- **Related Requirements:** REQ-013, REQ-014
- **Status:** Confirmed

---

## BR-009 — AI Recommendation Does Not Automatically Book

- **Type:** BR
- **Source:** AI feature scope
- **Priority:** Must
- **Statement:** An AI recommendation must not automatically create or confirm an appointment without the required booking and confirmation actions.
- **Related Requirements:** REQ-004, REQ-006, REQ-013, REQ-014
- **Status:** Confirmed

---

# 8. Constraints

## CON-001 — Minimum Supported Roles

- **Type:** CON
- **Statement:** The system must support at least Patient, Doctor, Receptionist, and Admin roles.
- **Source:** Project brief
- **Priority:** Must
- **Status:** Confirmed

---

## CON-002 — Mandatory Workflow

- **Type:** CON
- **Statement:** The project must support the workflow:

```text
Search Doctor → Book → Confirm → Check-in → Consult → Follow-up
```

- **Source:** Project brief
- **Priority:** Must
- **Status:** Confirmed

---

## CON-003 — AI Scope Limitation

- **Type:** CON
- **Statement:** AI functionality is limited to recommendation assistance and must not become a diagnostic or treatment-decision system.
- **Source:** Project brief
- **Priority:** Must
- **Status:** Confirmed

---

# 9. Assumptions

## ASM-001 — Clinic Schedule Data Exists

- **Type:** ASM
- **Statement:** Doctor and schedule data are available to the application.
- **Status:** Draft

---

## ASM-002 — User Identity Is Available

- **Type:** ASM
- **Statement:** The system can identify the authenticated Patient, Doctor, Receptionist, or Admin when performing role-specific operations.
- **Status:** Draft

---

# 10. Open Questions

The following points are not yet confirmed and must not be treated as final business rules.

## Q-001 — Appointment Cancellation

Can a patient cancel an appointment?

- **Status:** Open

## Q-002 — Appointment Rescheduling

Can a patient reschedule an existing appointment?

- **Status:** Open

## Q-003 — Check-in Window

How early or late can a patient check in relative to the appointment time?

- **Status:** Open

## Q-004 — Queue Ordering Policy

What determines queue order?

Possible factors may include appointment time, check-in time, priority, or another clinic rule.

- **Status:** Open

## Q-005 — Follow-up Definition

What exact information constitutes a follow-up record?

- **Status:** Open

## Q-006 — Notification Channels

Which notification channels are required?

Examples may include in-app notification, email, SMS, or other channels.

- **Status:** Open

## Q-007 — AI Recommendation Inputs

Which patient-provided constraints may be used for recommendations?

Examples may include specialty, preferred date, preferred time, doctor availability, or other explicitly defined constraints.

- **Status:** Open

## Q-008 — AI Recommendation Explanation

Should the system explain why a doctor or schedule was recommended?

- **Status:** Open

## Q-009 — Performance Target

What exact response-time target should be used for core interactions?

- **Status:** Open

---

# 11. Requirement Traceability Summary

| Requirement | Related Business Rules | Priority | Acceptance Criteria |
|---|---|---|---|
| REQ-001 | — | Must | AC-001-01, AC-001-02 |
| REQ-002 | — | Must | AC-002-01, AC-002-02 |
| REQ-003 | — | Should | TBD |
| REQ-004 | BR-001, BR-002 | Must | AC-004-01, AC-004-02 |
| REQ-005 | — | Must | TBD |
| REQ-006 | BR-003 | Must | AC-006-01, AC-006-02 |
| REQ-007 | BR-003, BR-004 | Must | TBD |
| REQ-008 | BR-004 | Must | TBD |
| REQ-009 | — | Must | TBD |
| REQ-010 | BR-005 | Must | TBD |
| REQ-011 | BR-006 | Must | TBD |
| REQ-012 | — | Must | TBD |
| REQ-013 | BR-007, BR-008, BR-009 | Should | AC-013-01, AC-013-02 |
| REQ-014 | BR-007, BR-008, BR-009 | Should | AC-014-01, AC-014-02 |

---

# 12. Self-check

- [x] Requirement IDs are unique.
- [x] Requirement types are explicitly identified.
- [x] Priority is defined.
- [x] Requirement statements are written in testable form.
- [x] Core booking workflow is represented.
- [x] AI scope is explicitly constrained.
- [x] Business rules are separated from functional requirements.
- [x] Open questions are separated from confirmed requirements.
- [x] At least two requirements have Given/When/Then acceptance criteria.
- [ ] Group review completed.
- [ ] All Draft requirements confirmed by the group.
- [ ] Open Questions resolved where required.

---

# 13. Evidence for Individual Report

The student responsible for this artifact should be able to demonstrate at least two requirements.

## Evidence 1 — REQ-004: Book Appointment

Explain:

1. Why REQ-004 is a Must requirement.
2. Which business rules constrain it.
3. How AC-004-01 proves the happy path.
4. How AC-004-02 proves the unavailable-slot case.

Trace:

```text
REQ-004
   ↓
BR-001 / BR-002
   ↓
AC-004-01 / AC-004-02
```

## Evidence 2 — REQ-013: AI-assisted Doctor Recommendation

Explain:

1. Why the AI feature exists.
2. What information the recommendation is allowed to use.
3. Why AI must not diagnose.
4. How the acceptance criteria handle insufficient information.

Trace:

```text
REQ-013
   ↓
BR-007 / BR-008 / BR-009
   ↓
AC-013-01 / AC-013-02
```

---

# 14. Status Policy

- **Draft:** Proposed but not yet confirmed by the group.
- **Confirmed:** Reviewed and accepted by the group.
- **Superseded:** Replaced by a newer requirement or decision.

Requirement IDs must not be reused for unrelated requirements.