# Django To-Do List Application

This project is a **user-based To-Do List web application** built with **Django**. It is an extended and enhanced version of the project presented in the step-by-step tutorial available at:  
https://www.youtube.com/watch?v=llbtoQTt4qw

The application allows users to **register, log in, and manage their own tasks**, with features such as task completion tracking, urgency flags, and search functionality.
It is implemented using **Django’s class-based generic views** together with the **built-in authentication system**, providing a clean, secure, and scalable structure that can be easily extended with additional features.

---

## Features

- User authentication (register, login, logout)
- Per-user task management
- Create, update, view, and delete tasks
- Mark tasks as **complete / incomplete**
- Mark tasks as **urgent**
- Task prioritization and ordering
- Search tasks by title
- Automatic login after registration

---

## Task Model

Each task contains the following fields:

- **User** – owner of the task
- **Title** – short description of the task
- **Description** – optional detailed text
- **Complete** – boolean flag indicating completion
- **Urgent** – boolean flag indicating priority
- **Created** – timestamp of creation

Tasks are ordered so that:
1. Incomplete tasks appear before completed tasks
2. Urgent tasks are prioritized among incomplete tasks

---

## Application Structure

### Models
- `Task`  
  Represents a single to-do item associated with a user.

### Views
- **Authentication**
  - `CustomLoginView` – user login
  - `RegisterPage` – user registration
  - `LogoutView` – user logout

- **Task Management**
  - `TaskList` – list of user tasks with search and ordering
  - `TaskDetail` – detailed view of a task
  - `TaskCreate` – create a new task
  - `TaskUpdate` – update an existing task
  - `TaskDeleteView` – delete a task

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

| URL Path | Description |
|--------|------------|
| `/login/` | User login |
| `/logout/` | User logout |
| `/register/` | User registration |
| `/` | Task list |
| `/task/<id>/` | Task detail |
| `/task-create/` | Create task |
| `/task-update/<id>/` | Update task |
| `/task-delete/<id>/` | Delete task |

---

## Authentication & Security

- Only authenticated users can access tasks
- Tasks are associated with individual users
- Users can only manage their own tasks
- Automatic redirection prevents logged-in users from accessing login/register pages

---

## Technologies Used

- Python
- Django
- Django Authentication System
- Class-Based Views (CBVs)
- HTML Templates

---

## Purpose

This project serves as:
- A practical example of Django CBVs
- A learning project for authentication and user-based data
- A foundation for extending features such as pagination, REST APIs, or task categories

---

## Possible Improvements

- Pagination for large task lists
- Case-insensitive search
- Task deadlines or priority levels
- REST API integration (Django REST Framework)
- UI enhancements

---

## License

This project is intended for educational and personal use.
