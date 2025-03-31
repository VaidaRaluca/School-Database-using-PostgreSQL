# School Database using PostgreSQL

## Overview
This project is a PostgreSQL-based school database that manages students, teachers, courses, and grades. It efficiently organizes academic records, attendance, and teacher-student relationships.

## Features
- Student management (registration, personal details, and enrollment)
- Teacher management (assignments, subjects taught, and contact details)
- Course management (subjects, enrollments, and grades)
- Attendance tracking

## Database Schema
The database consists of the following tables:

1. **adresa** (Addresses)
   - `id_adresa` (BIGSERIAL PRIMARY KEY)
   - `strada` (VARCHAR(20))
   - `numar` (INTEGER)
   - `localitate` (VARCHAR(20))

2. **elev** (Students)
   - `id_elev` (BIGSERIAL PRIMARY KEY)
   - `nume` (VARCHAR(20))
   - `prenume` (VARCHAR(20))
   - `data_nasterii` (DATE)
   - `id_adresa` (BIGINT, FOREIGN KEY references adresa(id_adresa))
   - `telefon` (VARCHAR(10))

3. **profesor** (Teachers)
   - `id_profesor` (BIGSERIAL PRIMARY KEY)
   - `nume` (VARCHAR(20))
   - `prenume` (VARCHAR(20))
   - `id_adresa` (BIGINT, FOREIGN KEY references adresa(id_adresa))
   - `mail` (VARCHAR(20))
   - `telefon` (VARCHAR(10))
   - `id_materie` (BIGINT, FOREIGN KEY references materie(id_materie))

4. **materie** (Subjects)
   - `id_materie` (BIGSERIAL PRIMARY KEY)
   - `nume` (VARCHAR(20))

5. **elev_materie** (Student-Subject Enrollment)
   - `id_elev` (BIGINT, FOREIGN KEY references elev(id_elev))
   - `id_materie` (BIGINT, FOREIGN KEY references materie(id_materie))

6. **elev_profesor** (Student-Teacher Relationship)
   - `id_elev` (BIGINT, FOREIGN KEY references elev(id_elev))
   - `id_profesor` (BIGINT, FOREIGN KEY references profesor(id_profesor))

7. **nota** (Grades)
   - `id_nota` (BIGSERIAL PRIMARY KEY)
   - `id_elev` (BIGINT, FOREIGN KEY references elev(id_elev))
   - `id_materie` (BIGINT, FOREIGN KEY references materie(id_materie))
   - `valoare` (INTEGER)
   - `data` (DATE)

8. **absenta** (Attendance)
   - `id_absenta` (BIGSERIAL PRIMARY KEY)
   - `id_elev` (BIGINT, FOREIGN KEY references elev(id_elev))
   - `data` (DATE)
   - `id_materie` (BIGINT, FOREIGN KEY references materie(id_materie))

## Installation
### Prerequisites
- PostgreSQL installed on your machine
- A PostgreSQL client (such as pgAdmin or psql CLI)

### Setup Steps
1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/school-database.git
   cd school-database
   ```
2. Create the database in PostgreSQL:
   ```sql
   CREATE DATABASE school_db;
   ```
3. Connect to the database:
   ```sh
   psql -U your_user -d school_db
   ```
4. Run the schema script:
   ```sh
   psql -U your_user -d school_db -f schema.sql
   ```

## Usage
- Use SQL queries to insert, update, delete, and retrieve data.
- Example: Retrieve all students enrolled in a specific subject
  ```sql
  SELECT elev.nume, elev.prenume, materie.nume 
  FROM elev 
  JOIN elev_materie ON elev.id_elev = elev_materie.id_elev 
  JOIN materie ON elev_materie.id_materie = materie.id_materie;
  ```

## Contributing
Feel free to fork this repository and submit pull requests with enhancements or bug fixes.

## License
This project is licensed under the MIT License.
