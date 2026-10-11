# Student Enrollment Management System

A web-based student enrollment management application built with **Python and Django**. The project supports three user roles—**administrator, professor, and student**—and provides role-specific workflows for managing courses, students, enrollment records, and academic results.

> **Project status:** Educational project / prototype. The application has not been verified for production use. Review the security and setup notes below before deploying it or publishing a copy of the development database.

## Features

### Administrator
- View and manage course records and their assigned professors.
- Add users and manage student and professor records.
- View student lists, professor lists, and enrollment information.
- Create and review enrollment records for students.
- Inspect course enrollment and results, including lists of students who have passed subjects.

### Professor
- View subjects assigned to the logged-in professor.
- Inspect students enrolled in a subject.
- Update student enrollment status (enrolled, passed, or failed).
- Review enrolled, passed, and failed students for a subject.

### Student
- View their personal enrollment sheet.
- See enrolled and available subjects.
- Enroll in a subject and access withdrawal flows.
- Review enrollment status for subjects.

Some functionality depends on the user's role and is protected by Django's login and role-check decorators.

## Tech Stack

| Layer | Technology |
| --- | --- |
| Backend | Python, Django 4.2.x |
| Frontend | Django Templates, HTML, CSS |
| Database | SQLite (development) |
| Authentication | Django authentication, custom user model |
| Data access | Django ORM |

## Application Design

The project follows Django's **Model–View–Template (MVT)** pattern:

- **Models** define users, subjects, and their enrollment relationships.
- **Views** handle HTTP requests, validation, database operations, and role-specific workflows.
- **Templates** render the pages shown to administrators, professors, and students.
- **Forms** support course and enrollment data entry.
- **URL routes** connect incoming requests to view functions.

### Core Models

- `Korisnici` — a custom user model extending Django's `AbstractUser`, including a role (`administrator`, `profesor`, or `student`) and student study status.
- `Predmeti` — a subject/course with a name, code, programme, ECTS credits, semester information, optional-course flag, and assigned professor.
- `StudentEnrollment` — a relationship between a student and a subject with status `Enrolled`, `Passed`, or `Failed`.

### Project Structure

```text
StudentEnrollmentApp/
├── EnrollmentApp/
│   ├── models.py
│   ├── views.py
│   ├── forms.py
│   ├── templates/
│   └── tests.py
├── project/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── static/
│   ├── css/
│   └── img/
├── manage.py
└── fixtures.json
```

## Running Locally

**Requirements:** Python, pip, and Django 4.2.x.

The Django application lives in the **`StudentEnrollmentApp/`** directory inside this repository.

1. Clone the repository and change into the Django application directory:

   ```bash
   git clone https://github.com/Ela1009/StudentEnrollmentApp.git
   cd StudentEnrollmentApp/StudentEnrollmentApp
   ```

2. Create and activate a *new* virtual environment (do not rely on an uploaded `venv` folder):

   **Windows PowerShell:**

   ```powershell
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

   **macOS/Linux:**

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. Install Django:

   ```bash
   python -m pip install "Django>=4.2,<4.3"
   ```

4. Review `project/settings.py` and configure a local-only Django `SECRET_KEY` and other environment-specific settings. Do not use the committed development key for deployment.

5. Apply migrations and start the development server:

   ```bash
   python manage.py migrate
   python manage.py runserver
   ```

6. Open **http://127.0.0.1:8000/cover/** or **http://127.0.0.1:8000/accounts/login/**.

**Important:** The checked archive does not include a verified reproducible dependency lockfile or a clean, empty-database setup procedure. A fresh installation may need the project's original migrations, suitable role-based test users, and/or additional setup. The optional `fixtures.json` is project data; inspect it before loading it. These commands are a starting point, not a claim that a clean installation was tested successfully.

## Role-Based Access

Views use Django's `@login_required` and `@user_passes_test` decorators to restrict many workflows to administrators, professors, or students. The custom user model stores the application role.


## Learning Outcomes

This project demonstrates working with the **Django MVT architecture**, custom authentication roles, Django ORM relationships, forms, templates, and server-rendered role-specific views.

---

**Purpose:** University programming project developed for learning and demonstrating Python/Django web application development.
