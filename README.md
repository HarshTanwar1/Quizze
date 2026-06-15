<h1 align="center">📝 Quizze — Online Quiz Portal</h1>

<p align="center">
  <em>A full-stack web platform that lets teachers conduct timed, course-wise online quizzes and gives students instant, automatically graded results</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/Django-3.1.7-092E20?style=for-the-badge&logo=django&logoColor=white" alt="Django" />
  <img src="https://img.shields.io/badge/MySQL-Database-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/Bootstrap-UI-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white" alt="Bootstrap" />
  <img src="https://img.shields.io/badge/jQuery-JS-0769AD?style=for-the-badge&logo=jquery&logoColor=white" alt="jQuery" />
</p>

<br>

## 🎯 Overview

**Quizze** is an online quiz platform built for colleges and schools. Teachers create courses, enroll students, and design course-wise quizzes with multiple-choice questions — all gated behind a time window they control. Students attempt quizzes within that window and receive **instantly graded results**, accessible to both students and teachers.

The project is backed by a carefully designed **relational schema** (modeled from an ER diagram) and demonstrates the full Django request → model → template lifecycle on a real MySQL database.

<br>

## ✨ Key Features

|     | Feature                 | Description                                                                       |
| --- | ----------------------- | --------------------------------------------------------------------------------- |
| 🔐  | **Dual Authentication** | Separate registration & login flows for **teachers** and **students**.            |
| 📚  | **Course Management**   | Teachers create courses and enroll registered students in them.                   |
| 🧠  | **Quiz Builder**        | Course-wise quizzes with multiple-choice questions (up to four options each).     |
| ⏱️  | **Timed Access**        | Quizzes are attemptable only within the date/time window set by the teacher.      |
| ⚡   | **Auto-Grading**        | Responses are scored against correct answers automatically — no manual marking.   |
| 📊  | **Instant Results**     | Results display immediately after a quiz ends, visible to students and teachers.  |
| 🛠️  | **Admin Panel**         | Django admin to manage students, teachers, courses, quizzes, questions & results. |

<br>

## 🧰 Tech Stack

| Layer         | Technologies                                                                     |
| ------------- | -------------------------------------------------------------------------------- |
| **Front-End** | HTML, CSS, JavaScript, Bootstrap, jQuery, Django Template Language               |
| **Back-End**  | Python, Django 3.1.7                                                             |
| **Database**  | MySQL — with `mysqlclient` / `mysql-connector-python` & `django-composite-field` |

<br>

## 🚀 Getting Started

**1. Clone the repository**

```bash
git clone https://github.com/HarshTanwar1/Quizze.git
cd Quiz
```

**2. Create and activate a virtual environment**

```bash
python -m venv venv
source venv/bin/activate      # On Windows: venv\Scripts\activate
```

**3. Install dependencies**

```bash
pip install django==3.1.7 mysqlclient mysql-connector-python django-composite-field
```

**4. Set up the MySQL database**

Create a database, then update the `DATABASES` block in `Quiz_App/settings.py` with your own credentials:

```sql
CREATE DATABASE quiz_db;
```

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'quiz_db',
        'USER': '<your-mysql-user>',
        'PASSWORD': '<your-mysql-password>',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
}
```

**5. Apply migrations**

```bash
python manage.py makemigrations
python manage.py migrate
```

**6. Create an admin (superuser) account**

```bash
python manage.py createsuperuser
```

**7. Run the development server**

```bash
python manage.py runserver
```

**8. Open the app** 👉 `http://127.0.0.1:8000/`
Admin panel 👉 `http://127.0.0.1:8000/admin/`

<br>

## 💡 What I Learned

- 🏗️ Building a complete **Django** project from scratch — project/app structure, URL routing, views, and the request/response cycle.
- 🗂️ Translating an **ER diagram** into Django **models** — foreign keys, composite/`unique_together` keys, and custom table names via `Meta`.
- 📝 Handling dynamic, multi-question input with **Django Forms & formsets** (`formset_factory`, `modelformset_factory`, `inlineformset_factory`).
- 🐬 Integrating **MySQL** as the backend and managing schema evolution through **migrations**.
- 🔑 Implementing **authentication, sessions, and authorization** to separate teacher and student capabilities.
- 🎨 Rendering data-driven pages with the **Django Template Language**, styled with HTML/CSS, Bootstrap, and jQuery.
- ⏳ Implementing **time-based logic** (quiz availability windows) and server-side validation.

<br>

## 🔮 Future Improvements

- ✅ **Validation & UX:** stronger client/server validation, friendlier errors, and a responsive, modernized UI.
- 🧩 **Features:** more question types (true/false, multi-select, descriptive), a question bank, quiz randomization, per-question timers, and analytics/leaderboards.
- 📧 **Notifications:** email results and quiz reminders via Django's email backend / SMTP.
- 🧪 **Quality:** expose **REST APIs** (Django REST Framework) for a decoupled front end.

<br>

## 🗃️ Database Design

<details>
<summary><strong>ER Model Description</strong> (click to expand)</summary>

<br>

- If the teacher and student have an existing account they can log in; otherwise they can register and create their account.
- Users set up their own username and password.
- The teacher enrolls students into their respective courses.
- The teacher can create quizzes and link them to their courses. Every quiz has a unique ID.
- Students enrolled in a course can view details of upcoming and previous quizzes.
- Each question of a quiz has a unique ID.
- A student's response to each question is uniquely identified by the student's roll number and the question's ID.

**Entities and Attributes**

| Entity        | Attributes                                                          | Primary Key                 |
| ------------- | ------------------------------------------------------------------- | --------------------------- |
| **Students**  | RollNo, Name, Mail, Password                                        | RollNo                      |
| **Courses**   | Course_ID, Course_Name                                              | Course_ID                   |
| **Teacher**   | Teacher_ID, Name, Mail, Password                                    | Teacher_ID                  |
| **Quiz**      | quiz_id, Course_ID, duration, date, start_time, end_time, quiz_name | quiz_id                     |
| **Questions** | q_id, quiz_id, question, ans, opt1, opt2, opt3, opt4                | q_id                        |
| **Responses** | RollNo, q_id, response                                              | (RollNo, q_id) composite    |
| **Results**   | RollNo, quiz_id, marks                                              | (RollNo, quiz_id) composite |

</details>

### ER Model

![ER Model](https://github.com/avnishranwa7/Quiz/blob/main/ER%20Model.png)

### Relational Schema

![Relational Schema](https://github.com/avnishranwa7/Quiz/blob/main/Relational%20Schema.jpg)

<br>

---

<div align="center">

⭐ _If you found this project helpful or interesting, consider giving it a star!_ ⭐

</div>
