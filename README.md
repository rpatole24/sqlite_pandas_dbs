# Assignment 2 : Sqlite and Basic Queries

**Student Info**  
Name: Rujula Patole

**Repo:** `sqlite_pandas_dbs`

## Overview 
This project builds an SQLite database (clinic_simple.db) from a SQL schema and loads patient data from data/patients.csv using Pandas and SQLAlchemy. After loading, single-table queries in DB Browser for SQLite verify total rows, top primary diagnoses, recent office-visit CPTs, approximate ages, and basic data quality. The repo is organized as sql/, data/, and src/ so anyone can recreate the database and reproduce results.


---

## Run Steps (How to Recreate the Database)

1. **Open the project**
   - Open VS Code.
   - Go to File > Open Folder and select your repository that contains `src/`, `sql/`, and `data/`.
   - Confirm in the Explorer that `src/`, `sql/`, and `data/` are visible at the top level.

2. **Open the terminal at the repo root**
   - Go to View > Terminal to open the integrated terminal.
   - Verify the terminal path ends with your repo folder name.

3. **Create a virtual environment**
   - Run: `python3 -m venv .venv`
   - Activate: `source .venv/bin/activate`
   - Confirm the prompt now begins with `(.venv)`.

4. **Install dependencies**
   - Run: `python3 -m pip install -r requirements.txt`
   - Wait for confirmation that `pandas` and `SQLAlchemy` were installed successfully.

5. **Confirm required files are present**
   - Ensure these files exist with the exact paths:
     - `src/create_db.py`
     - `src/import_csv.py`
     - `sql/schema.sql`
     - `sql/analysis.sql`
     - `data/patients.csv`

6. **Create the SQLite database from the schema**
   - Run: `python3 src/create_db.py`
   - Expect a message indicating the database was created.
   - Verify `clinic_simple.db` appears at the repo root in the Explorer.

7. **Import the CSV into the `patients` table**
   - Run: `python3 src/import_csv.py`

8. **Open the database in DB Browser for SQLite**
   - Launch DB Browser for SQLite.
   - Choose Open Database… and select the `clinic_simple.db` file in your repo.
   - Go to Browse Data and choose the `patients` table to confirm rows are present.

9. **Run the assignment queries**
   - Go to Execute SQL in DB Browser.
   - Open the file `sql/analysis.sql`.
   - Click Run to execute the queries.
   - Capture screenshots or copy text outputs for queries A–E to include in your README.


---

## Query Results

### A) Row Count
- **Description:**
  - Returns the total number of rows in the patients table (how many patients are in the roster) to confirm the CSV loaded correctly.
- **Explanation:** 
  - Shows that there are 500 patients in the roster, and 500 rows of information.
 <img width="1108" height="801" alt="SQLHW2QUERYA" src="https://github.com/user-attachments/assets/df70b4fd-955d-4fd7-82f5-7f299b56f98e" />


### B) Top Primary Diagnoses by Count
- **Description:**
  - Groups patients by primary_icd10, counts how many per code, and sorts from most to least common.
- **Explanation:**
  - The most frequent diagnoses are I10 (81), E11.9 (73), and E78.5 (62), followed by J45.909 (46) and F41.9 (33). This highlights the leading conditions represented in the roster.
- <img width="1113" height="869" alt="SQLHW2QUERYB" src="https://github.com/user-attachments/assets/4089add7-951b-4b5a-8aff-0f58e6d86a74" />


### C) Office-visit CPTs since Jan 1, 2025 (CPT codes starting with 992)
- **Description:**
  - Filters to encounters with last_cpt and last_visit_dt, ordered by the most recent visit date.
- **Explanation:**
  - 94 rows matched, these are recent office-visit (E/M) encounters since 2025-01-01, listed newest first to emphasize current utilization.
- <img width="1341" height="1063" alt="SQLHW2QUERYC" src="https://github.com/user-attachments/assets/47143ea1-0907-463d-8597-08cd4af848d5" />


### D) Age (approx) at last visit for the 5 oldest patients
- **Description:**
  - Description: Calculates approximate age in years using julianday and returns the five oldest patients, sorted by age (descending).
- **Explanation:**
  - The top five oldest patients are all about 85 years old. This provides a quick demographic snapshot of the 5 oldest seniors they have.
<img width="878" height="882" alt="SQLHW2QUERYD" src="https://github.com/user-attachments/assets/25e8aa97-974e-413b-b5a2-221b3c65440a" />


### E) Quick data quality check: any blank codes?
- **Description:**
  - Returns any records where primary_icd10 or last_cpt to flag missing code values.
- **Explanation:**
  - 0 rows returned, no blank ICD-10 or CPT codes detected, indicating these required fields are complete.
- <img width="486" height="884" alt="SQLHW2QUERYE" src="https://github.com/user-attachments/assets/e4d68633-feed-400c-84e2-ad4ef32dfdc2" />


