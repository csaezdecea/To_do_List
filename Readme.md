# Django To-Do List Application

This project is a **user-based To-Do List web application** built with **Django**. It is an extended and enhanced version of the project presented in the step-by-step tutorial available at:
[https://www.youtube.com/watch?v=llbtoQTt4qw](https://www.youtube.com/watch?v=llbtoQTt4qw)

The application allows users to **register, log in, and manage their own tasks**, with features such as task completion tracking, urgency flags, and search functionality.
It is implemented using **Django’s class-based generic views** together with the **built-in authentication system**, providing a clean, secure, and scalable structure that can be easily extended with additional features.

---

## Features

* User authentication (register, login, logout)
* Per-user task management
* Create, update, view, and delete tasks
* Mark tasks as **complete / incomplete**
* Mark tasks as **urgent**
* Task prioritization and ordering
* Search tasks by title
* Automatic login after registration

---

## Task Model

Each task contains the following fields:

* **User** – owner of the task
* **Title** – short description of the task
* **Description** – optional detailed text
* **Complete** – boolean flag indicating completion
* **Urgent** – boolean flag indicating priority
* **Created** – timestamp of creation

Tasks are ordered so that:

1. Incomplete tasks appear before completed tasks
2. Urgent tasks are prioritized among incomplete tasks

---

## Application Structure

### Models

* `Task`
  Represents a single to-do item associated with a user.

### Views

* **Authentication**

  * `CustomLoginView` – user login
  * `RegisterPage` – user registration
  * `LogoutView` – user logout

* **Task Management**

  * `TaskList` – list of user tasks with search and ordering
  * `TaskDetail` – detailed view of a task
  * `TaskCreate` – create a new task
  * `TaskUpdate` – update an existing task
  * `TaskDeleteView` – delete a task

All task-related views require authentication.

---

## Task Ordering Logic

Tasks are ordered according to the following priority:

1. Incomplete & urgent
2. Incomplete & not urgent
3. Completed tasks

This ensures that the most important pending tasks are displayed first.

---

## Search Functionality

Users can search for tasks by title using a search input.
The task list is dynamically filtered based on the provided search string.

---

## URL Routes

| URL Path             | Description       |
| -------------------- | ----------------- |
| `/login/`            | User login        |
| `/logout/`           | User logout       |
| `/register/`         | User registration |
| `/`                  | Task list         |
| `/task/<id>/`        | Task detail       |
| `/task-create/`      | Create task       |
| `/task-update/<id>/` | Update task       |
| `/task-delete/<id>/` | Delete task       |

---

## Authentication & Security

* Only authenticated users can access tasks
* Tasks are associated with individual users
* Users can only manage their own tasks
* Automatic redirection prevents logged-in users from accessing login/register pages

---

## Technologies Used

* Python
* Django
* Django Authentication System
* Class-Based Views (CBVs)
* HTML Templates

---

## Purpose

This project serves as:

* A practical example of Django CBVs
* A learning project for authentication and user-based data
* A foundation for extending features such as pagination, REST APIs, or task categories

---

## Possible Improvements

* Pagination for large task lists
* Case-insensitive search
* Task deadlines or priority levels
* REST API integration (Django REST Framework)
* UI enhancements

---

## Environment Setup & SECRET_KEY

To keep your secret key safe and avoid committing it to GitHub, follow these steps:

### 1. Install `python-decouple` (if not already installed)

```bash
pip install python-decouple
```

---

### 2. Generate a new SECRET_KEY

Run the following command in your terminal:

```bash
python3 -c "from django.core.management.utils import get_random_secret_key
print(get_random_secret_key())"
```

* This will print a random secret key, for example:

```
b3v@9t$1x!p2q^8r&y7m*e0s+z6u%f4w
```

---

### 3. Create a `.env` file in the project root

```bash
nano .env
```

Add your new secret key:

```
SECRET_KEY=b3v@9t$1x!p2q^8r&y7m*e0s+z6u%f4w
```

Save and exit.

---

### 4. Update `settings.py` to use the secret from `.env`

Replace the old hardcoded secret:

```python
SECRET_KEY = 'your_old_secret_key'
```

with:

```python
from decouple import config

SECRET_KEY = config('SECRET_KEY')
```

---

### 5. Ensure `.env` is ignored by Git

```bash
echo ".env" >> .gitignore
```

* This ensures the secret key is **never pushed to GitHub**.

---

### 6. Run the Django server

Now your project can run safely on any machine:

```bash
python3 manage.py runserver
```

* Django will read the secret key from `.env`.

---

## License

This project is intended for educational and personal use.
