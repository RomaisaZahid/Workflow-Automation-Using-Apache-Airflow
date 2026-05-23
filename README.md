**Workflow Automation Using Apache Airflow & Docker**:

This project is about automating data processing using Apache Airflow and Docker.
It includes two ETL pipelines (Extract, Transform, Load) that automatically collect, process, and store data.

**Project Overview**:
The project shows how automated workflows work in real-life data engineering.
There are two pipelines:
**Student Data ETL Pipeline**:
Processes student data.
Calculates grades and performance levels.
Stores the final data in a database.
**Employee Multi-File ETL Pipeline**:
Combines employee data from different departments.
Calculates bonuses and salary categories.
Creates a final processed employee file.

**Technologies Used**:
Apache Airflow → For workflow automation and scheduling.
Docker & Docker Compose → To run services in containers.
WSL 2 → Linux environment on Windows.
Python & Pandas → For data processing.
SQLite3 → Database storage.
PostgreSQL → Airflow metadata database.
Redis → Message broker service.

**Pipeline Details**:
**1. Student Data ETL Pipeline**:
**Data Source**:
data/data.csv
**Workflow**:
extract_task → transform_task → load_task
**What This Pipeline Does**:
Reads student data from a CSV file.
Converts text into proper format (capital letters where needed).
Assigns grades:
A = 85 or above
B = 70–84
C = 50–69
F = below 50
Adds performance labels:
Excellent
Good
Average
Poor
Removes failed students from the final data.
Saves processed data into the SQLite database etl.db in the students table.

**2. Employee Multi-File ETL Pipeline**:
**Data Sources**:
data/hr.csv
data/it.csv
data/finance.csv
**Workflow**:
extract_task → transform_task → load_task
**What This Pipeline Does**:
Reads employee data from multiple department files.
Adds a department column to identify where each record came from.
Merges all employee data into one dataset.
Calculates:
10% bonus
Total salary
Categorizes employees:
High = 75k or above
Medium = 60k–74,999
Low = below 60k
Removes low-category employees.
Sorts employees by highest salary.
Saves final output into final_employees.csv.

**Scheduling & Error Handling**:
**Automatic Scheduling**:
Both pipelines run automatically every day at 9:00 AM using:
schedule_interval='0 9 * * *'
**Additional Settings**:
catchup=False
Prevents old missed tasks from running automatically.
**Fault Tolerance**:
If a task fails:
Airflow retries it 2 times.
Waits 2 minutes between retries.

**Installation & Running the Project**:
Requirements
Windows 10/11,
WSL 2 enabled,
Docker Desktop installed with WSL 2 integration.
