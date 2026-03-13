# Automated Course Scheduling System 📅

An intelligent local desktop application designed to enable university departments to create weekly course schedules in an error-free and optimized manner.

---

## 1. Introduction
### 1.1 Purpose of the Document
To define the requirements of a local software that enables any university department to create a weekly course schedule in an error-free and optimized manner.

### 1.2 Scope of the Project
The software takes course curriculum data, lecturer availability and preferences, classroom capacities, and student cohort/semester enrollments as input. Using an optimization algorithm (**Genetic Algorithm, Tabu Search, etc.**), it generates a weekly timetable that satisfies all constraints. If the solution set is empty, it warns the user.

---

## 2. General Description
### 2.1 Product Perspective
Standalone desktop application. No internet connection required. All data is stored in local files (**JSON, CSV, or SQLite**).

### 2.2 User Characteristics
The system is designed for the **Department Coordinator**. Technical knowledge level: Intermediate.

### 2.3 Assumptions
* Data uploaded (course list, classroom list) is in the correct format.
* The hardware (RAM/CPU) is sufficient for optimization processes.

### 2.4 Constraints
#### 2.4.1 Hard Constraints (Mandatory)
* **Same Classroom:** No two courses in the same room at the same time.
* **Same Lecturer:** A lecturer cannot teach two different courses at once.
* **Student Conflict:** Cohorts cannot have two mandatory courses scheduled simultaneously.
* **Capacity:** Enrollment cannot exceed classroom capacity.
* **Lecturer Preferences:** Prioritizes preferences of visiting lecturers.
* **Balance:** Students should not have more than 3 courses per day.
* **Lunch Break:** Continuous 1-hour break between 12:00 - 14:00.

#### 2.4.2 Soft Constraints (Preferred)
* **Time Interval:** Courses should be distributed to the early hours of the day.

---

## 3. Functional Requirements
### 3.1 Data Importing and Management
* **FR-01 (File Transfer):** Upload course/lecturer/classroom data in **Excel (XLSX) or CSV**.
* **FR-02 (Manual Data Editing):** Interface-based minor corrections.
* **FR-03 (Constraint Definition):** Define suitable working days and time slots.

### 3.2 Algorithm and Optimization
* **FR-04 (Auto Generation):** Must satisfy 100% of "Hard Constraints."
* **FR-05 (Variation):** Uses time-dependent seed for different valid alternatives.
* **FR-06 (Manual Editing):** Users can manually edit the schedule post-generation.
* **FR-07 (Real-Time Validation):** Identifies and visualizes violations during manual edits.
* **FR-08 (Contradiction Analysis):** Feedback provided if constraints are mathematically impossible.

### 3.3 Output Management
* **FR-09 (Saving):** Saves generated schedules to a local SQL database.
* **FR-10 (Exporting):** Downloadable **PDF or Excel** tables.

---

## 4. Non-Functional Requirements
* **Performance:** Results in 1-2 minutes for medium-sized departments.
* **Usability:** Easy installation (Single-click .exe or .jar). Descriptive error messages.
* **Reliability:** Validation for incorrect/missing data (e.g., zero capacity).
* **Data Security:** All operations occur within RAM; no cloud/external server communication.

---

## 5. Use-Case Flow
### Main Flow: Generate Automated Schedule
1.  **Initiate Import:** Coordinator uploads classroom, course, and enrollment files.
2.  **Data Validation:** System confirms data format.
3.  **Configuration:** Coordinator sets academic terms and time slots.
4.  **Execute Optimization:** Click "Generate Schedule."
5.  **Review:** Visual preview of the timetable.
6.  **Editing:** Manual adjustments with real-time constraint validation.
7.  **Saving:** Automatic SQL save.
8.  **Finalize:** Export to PDF or Excel.

---

### ⚠️ Exception Handling
* **Invalid Data Format:** System halts import and highlights the specific error (e.g., "Non-numeric capacity").
* **Impossible Scenario:** Algorithm generates a **Conflict Report** highlighting the bottleneck.
* **Timeout:** Prompts user to continue or relax "Soft Constraints" for a near-optimal solution.
